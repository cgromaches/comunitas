<template>
  <router-view />
</template>

<script>
export default {
  name: 'App',
  created() {
    let pushed = false;
    const currentPath = this.$router.history.current.path;

    if (window.localStorage.getItem('authenticated') === 'false') {
      pushed = true;
      this.$router.push('/');
    }

    if (currentPath === '/' || currentPath === '/app' || currentPath === '#'){
      pushed = true;
      this.$router.push('/app/landing');
    }

    if(currentPath === '/dao' || JSON.stringify(currentPath).indexOf('/dao') !== -1) {
      pushed = true;
      window.localStorage.setItem('authenticated', true);
      this.$router.push('/dao/dashboard');
    }

    if(!pushed){
      this.$router.push(currentPath);
    }
  },
};
</script>

<style src="./styles/theme.scss" lang="scss" />
