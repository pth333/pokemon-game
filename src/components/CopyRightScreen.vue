<template>
  <div class="copyright">
    <p>
      This is game owned by Hiếu đzai in Vue 3 course for begginers -
      <a href="https://www.facebook.com/profile.php?id=100081899021971"
        >Hiếu đzai</a
      >
    </p>
  </div>
</template>
<style lang="css" scoped>
.copyright {
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  bottom: 1.5rem;
  color: var(--light);
  z-index: 3;
  font-size: 1.5rem;
}

.copyright a {
  color: #f4dc26;
}
</style>
