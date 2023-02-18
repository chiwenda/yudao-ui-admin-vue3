<!--
 * @Author: chiwenda 48881696+chiwenda@users.noreply.github.com
 * @Date: 2023-02-19 00:15:59
 * @LastEditors: chiwenda 48881696+chiwenda@users.noreply.github.com
 * @LastEditTime: 2023-02-19 00:47:59
 * @FilePath: /yudao-ui-admin-vue3/src/views/Login/components/ResetPasswordForm.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
<template>
  <el-form
    :model="loginData.loginForm"
    :rules="rules"
    label-position="top"
    class="login-form"
    label-width="120px"
    size="large"
    v-show="getShow"
    ref="formRestPasswordLogin"
  >
    <el-row style="margin-left: -10px; margin-right: -10px">
      <!-- 租户名 -->
      <el-col :span="24" style="padding-left: 10px; padding-right: 10px">
        <el-form-item>
          <LoginFormTitle style="width: 100%" />
        </el-form-item>
      </el-col>

      <!-- 登录按钮 / 返回按钮 -->
      <el-col :span="24" style="padding-left: 10px; padding-right: 10px">
        <el-form-item>
          <XButton
            :loading="loginLoading"
            type="primary"
            class="w-[100%]"
            :title="t('login.login')"
          />
        </el-form-item>
      </el-col>
      <el-col :span="24" style="padding-left: 10px; padding-right: 10px">
        <el-form-item>
          <XButton
            :loading="loginLoading"
            class="w-[100%]"
            :title="t('login.backLogin')"
            @click="handleBackLogin()"
          />
        </el-form-item>
      </el-col>
    </el-row>
  </el-form>
</template>
<script setup lang="ts">
import { unref } from 'vue'
import { useLoginState, LoginStateEnum } from './useLogin'
const { t } = useI18n()
const { getLoginState, handleBackLogin } = useLoginState()
const getShow = computed(() => unref(getLoginState) === LoginStateEnum.RESET_PASSWORD)
const loginLoading = ref(false)
const rules = {
  tenantName: [required],
  mobileNumber: [required],
  code: [required]
}
const loginData = reactive({
  codeImg: '',
  tenantEnable: import.meta.env.VITE_APP_TENANT_ENABLE,
  token: '',
  loading: {
    signIn: false
  },
  loginForm: {
    uuid: '',
    tenantName: '芋道源码',
    mobileNumber: '',
    code: ''
  }
})
</script>
