<template>
  <b-navbar
    wrapper-class=""
    class="header h-[75px] max-[1023px]:fixed max-[1023px]:top-0  max-[1023px]:z-[60] max-[1023px]:bg-black  max-[1023px]:py-4 2xl:py-3  max-[1023px]:w-full   max-[1023px]:items-center  max-[1023px]:justify-between max-[1023px]:px-4  lg:fixed lg:top-0  lg:z-[60] lg:bg-black  lg:py-2 lg:2xl:py-3  lg:w-full lg:flex lg:items-center lg:justify-between  lg:px-10 lg:h-[75px]"
  >
    <template slot="brand">
      <b-navbar-item tag="router-link" to="/" data-test="toronodo_main_page" active-class="">
        <Logo />
      </b-navbar-item>
    </template>
    <template
      slot="start"
      class="btn-gradient inline-flex items-center justify-center p-2 rounded-md text-white"
    >
      <!-- <b-navbar-item
        v-if="isEnabledGovernance"
        tag="router-link"
        to="/governance"
        data-test="voting_link"
        :active="$route.path.includes('governance')"
        class="has-tag"
      >
        {{ $t('Home') }} <span v-if="hasActiveProposals" class="navbar-item--tag"></span>
      </b-navbar-item>
      <b-navbar-item tag="router-link" class="has-tag" to="/compliance" data-test="compliance_link">
        {{ $t('DApp') }}
      </b-navbar-item>-->
      <b-navbar-item
        tag="router-link"
        class="has-tag lg:ml-6 text-fonst text-emerald-500 text-xl font-bold logos-header"
        to="/"
      >
        {{ $t('Home') }}
      </b-navbar-item>
      <b-navbar-item
        tag="router-link"
        class="has-tag lg:ml-6 text-fonst text-emerald-500 text-xl font-bold logos-header"
        to="/dapp"
      >
        {{ $t('DApp') }}
      </b-navbar-item>
      <b-navbar-item
        tag="router-link"
        class="has-tag lg:ml-6 text-fonst text-emerald-500 text-xl font-bold logos-header"
        to="/"
      >
        {{ $t('Docs') }}
      </b-navbar-item>
      <!--  <b-navbar-item
        href="https://docs.toronodo.cash"
        target="_blank"
        data-test="docs_link"
        rel="noopener noreferrer"
        class="has-tag"
      >
        <b-icon icon="open-book" size="is-small" class="mr-1" />
        <span>{{ $t('docs') }}</span>
      </b-navbar-item>-->
    </template>
    <template slot="end">
      <b-navbar-item tag="div">
        <div class="buttons">
          <network-navbar-icon />
          <metamask-navbar-icon data-test="metamask_connection_state" />
          <!-- <indicator data-test="note_account_connection_state" /> 
          <b-button
            icon-left="settings"
            type="is-primary"
            outlined
            data-test="button_settings"
            @mousedown.prevent
            @click="onAccount"
          >
            {{ $t('settings') }}
          </b-button>-->
        </div>
      </b-navbar-item>
    </template>
  </b-navbar>
</template>

<script>
import { mapState, mapGetters } from 'vuex'
import Logo from '@/components/Logo'
// import { Indicator } from '@/modules/account'
import MetamaskNavbarIcon from '@/components/MetamaskNavbarIcon'
import NetworkNavbarIcon from '@/components/NetworkNavbarIcon'

export default {
  components: {
    Logo,
    // Indicator,
    NetworkNavbarIcon,
    MetamaskNavbarIcon
  },
  data() {
    return {
      isActive: false
    }
  },
  computed: {
    ...mapGetters('metamask', ['netId', 'isLoggedIn']),
    ...mapGetters('governance/gov', ['isEnabledGovernance']),
    ...mapState('governance/gov', ['hasActiveProposals'])
  },
  methods: {
    onAccount() {
      this.$router.push('/account')
    }
  }
}
</script>
