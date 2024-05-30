<template>
  <LoginFormTitle class="" />
  <ConfigProvider
    :theme="{
        algorithm: defaultAlgorithm,
      }">
    <Form
      class="p-4"
      :model="formData"
      :rules="getFormRules"
      ref="formRef"
      @keypress.enter="handleLogin"
    >
      <FormItem name="account" class="">
        <Input
          size="large"
          v-model:value="formData.account"
          :placeholder="t('sys.login.userName')"
          class="fix-auto-fill"
        />
      </FormItem>
      <FormItem name="password" class="">
        <InputPassword
          size="large"
          visibilityToggle
          v-model:value="formData.password"
          :placeholder="t('sys.login.password')"
        />
      </FormItem>

      <ARow class="">
        <ACol :span="12">
          <FormItem>
            <!-- No logic, you need to deal with it yourself -->
            <Checkbox v-model:checked="rememberMe" size="small">
              {{ t('sys.login.rememberMe') }}
            </Checkbox>
          </FormItem>
        </ACol>
        <ACol :span="12">
          <!--        <FormItem :style="{ 'text-align': 'right' }">
                    &lt;!&ndash; No logic, you need to deal with it yourself &ndash;&gt;
                    <Button type="link" size="small" @click="setLoginState(LoginStateEnum.RESET_PASSWORD)">
                      {{ t('sys.login.forgetPassword') }}
                    </Button>
                  </FormItem>-->
        </ACol>
      </ARow>

      <FormItem class="">
        <Button type="primary" size="large" block @click="handleLogin" :loading="loading">
          {{ t('sys.login.loginButton') }}
        </Button>
        <!-- <Button size="large" class="mt-4 enter-x" block @click="handleRegister">
          {{ t('sys.login.registerButton') }}
        </Button> -->
      </FormItem>
    </Form>
  </ConfigProvider>

</template>
<script lang="ts" setup>
  import { Greet } from '../../../../wailsjs/go/main/App.js';
  import { reactive, ref, unref, computed } from 'vue';

  import { Checkbox, Form, Input, Row, Col, Button, Divider, ConfigProvider, theme } from 'ant-design-vue';
  const { defaultAlgorithm } = theme;
  import {
    GithubFilled,
    WechatFilled,
    AlipayCircleFilled,
    GoogleCircleFilled,
    TwitterCircleFilled,
  } from '@ant-design/icons-vue';
  import LoginFormTitle from './LoginFormTitle.vue';

  import { useI18n } from '@/hooks/web/useI18n';
  import { useMessage } from '@/hooks/web/useMessage';

  import { useUserStore } from '@/store/modules/user';
  import { LoginStateEnum, useLoginState, useFormRules, useFormValid } from './useLogin';
  import { useDesign } from '@/hooks/web/useDesign';
  //import { onKeyStroke } from '@vueuse/core';

  const ACol = Col;
  const ARow = Row;
  const FormItem = Form.Item;
  const InputPassword = Input.Password;
  const { t } = useI18n();
  const { notification, createErrorModal } = useMessage();
  const { prefixCls } = useDesign('login');
  const userStore = useUserStore();

  const { setLoginState, getLoginState } = useLoginState();
  const { getFormRules } = useFormRules();

  const formRef = ref();
  const loading = ref(false);
  const rememberMe = ref(false);

  const formData = reactive({
    account: 'zfc',
    password: '123456',
  });

  const { validForm } = useFormValid(formRef);

  //onKeyStroke('Enter', handleLogin);
  async function handleLogin() {
    const data = await validForm();
    if (!data) return;
    try {
      loading.value = true;
      // window.go.main.App.Greet('abc').then((res) => {
      //   console.log(333333, res)
      // })
      /*Greet('abc').then(res => {
        console.log(333333, res)
      })*/
      const userInfo = await userStore.login({
        password: data.password,
        username: data.account,
        mode: 'none', //不要默认的错误提示
      });
    } catch (error) {
      createErrorModal({
        title: t('sys.api.errorTip'),
        content: (error as unknown as Error).message || t('sys.api.networkExceptionMsg'),
        getContainer: () => document.body.querySelector(`.${prefixCls}`) || document.body,
      });
    } finally {
      loading.value = false;
    }
  }
</script>
