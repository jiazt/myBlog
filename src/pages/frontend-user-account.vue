<template>
    <div class="main wrap clearfix">
        <div class="main-left">
            <div class="home-feeds cards-wrap">
                <div class="settings-main card">
                    <div class="settings-main-content">
                        <a-input title="昵称">
                            <input type="text" v-model="form.username" placeholder="昵称" class="base-input" name="username">
                            <span class="input-info error">请输入昵称</span>
                        </a-input>
                        <a-input title="邮箱">
                            <input type="text" v-model="form.email" placeholder="邮箱" class="base-input" name="email">
                            <span class="input-info error">请输入邮箱</span>
                        </a-input>
                    </div>
                    <!-- <div class="settings-footer clearfix">
                        <a href="javascript:;" class="btn btn-blue">保存设置</a>
                    </div> -->
                </div>
            </div>
        </div>
        <div class="main-right">
            <account></account>
        </div>
    </div>
</template>

<script>
// import api from '~api'
import metaMixin from '~mixins'
import checkUser from '~mixins/check-user'
import account from '../components/aside-account.vue'
import aInput from '../components/_input.vue'

export default {
    name: 'frontend-user-account',
    components: {
        account,
        aInput
    },
    mixins: [metaMixin, checkUser],
    data() {
        return {
            form: {
                username: '',
                email: ''
            }
        }
    },
    mounted() {
        this.getUser()
    },
    methods: {
        async getUser() {
            const {
                data: { code, data }
            } = await this.$store.$api.get('frontend/user/account')
            if (code === 200) {
                this.form.username = data.username
                this.form.email = data.email
            }
        }
    },
    metaInfo() {
        return {
            title: '帐号 - 威震天',
            meta: [{ vmid: 'description', name: 'description', content: '威震天' }]
        }
    }
}
</script>
