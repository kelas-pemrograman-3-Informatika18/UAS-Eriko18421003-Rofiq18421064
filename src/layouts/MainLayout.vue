<template>
  <q-layout view="lHh Lpr lFf">
    <q-header class="bg-white text-blue-grey-14">
      <q-toolbar>
        <q-btn dense flat round @click="leftDrawerOpen = !leftDrawerOpen" icon="menu"/>
        <q-space></q-space>
        <q-btn flat round>
          <q-avatar>
            <img src="https://cdn.quasar.dev/img/avatar.png">
          </q-avatar>
          <q-menu>
          <q-list style="min-width: 100px">
            <q-separator />
            <q-separator />
            <q-item clickable v-close-popup>
              <q-item-section>Profile</q-item-section>
            </q-item>
            <q-separator />
            <q-item clickable v-close-popup @click="logout()">
              <q-item-section>Logout</q-item-section>
            </q-item>
          </q-list>
        </q-menu>
        </q-btn>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      :breakpoint="500"
      content-class="text-white bg-primary"
    >
      <q-scroll-area class="fit">
        <q-list>
          <q-item class="justify-center text-center q-mb-md q-mt-md">
            <div>
              <q-avatar size="120px">
                <img src="https://cdn.quasar.dev/img/avatar.png">
              </q-avatar>
              <div class="text-weight-bold q-mt-md"> {{ $q.localStorage.getItem('dataUser').namaLengkap }}</div>
              <div>Aplikasi Penjualan Obat</div>
            </div>
          </q-item>

          <q-item clickable active-class="active" v-ripple exact :to="{ name: 'dashboardAdmin' } ">
            <q-item-section avatar>
              <q-icon name="dashboard"/>
            </q-item-section>
            <q-item-section>
              <q-item-label>Dashboard</q-item-label>
            </q-item-section>
          </q-item>
          <q-item clickable active-class="active" v-ripple exact :to="{ name: 'dataObat' } ">
            <q-item-section avatar>
              <q-icon name="dashboard"/>
            </q-item-section>
            <q-item-section>
              <q-item-label>Data Obat</q-item-label>
            </q-item-section>
          </q-item>
          <q-item clickable active-class="active" v-ripple exact :to="{ name: 'inputObat' } ">
            <q-item-section avatar>
              <q-icon name="input"/>
            </q-item-section>
            <q-item-section>
              <q-item-label>Input Obat</q-item-label>
            </q-item-section>
          </q-item>
          <q-item clickable active-class="active" v-ripple exact :to="{ name: 'dataUser' } ">
            <q-item-section avatar>
              <q-icon name="supervisor_account"/>
            </q-item-section>
            <q-item-section>
              <q-item-label>Data User</q-item-label>
            </q-item-section>
          </q-item>

      </q-list>
      </q-scroll-area>
    </q-drawer>

    <q-page-container class="bg-grey-1">
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  name: 'MainLayout',

  data () {
    return {
      leftDrawerOpen: false
    }
  },
  methods: {
    logout () {
      this.$q.localStorage.remove()
      this.$router.push({ name: 'loginPage' })
    }
  }
}
</script>
<style scoped>
.active {
  color: #000000;
  background: #fafafa;
  padding-right: 10px;
}
</style>
