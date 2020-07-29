<template>
  <section style="padding: 20px;">
    <h5>Vue App</h5>
    <div style="color: red;">
      <p>
        子应用修改，基座会加载么(gggggg)
      </p>
    </div>
  </section>
</template>
<script>
export default {
  name: "Home",
  beforeRouteEnter(to,from,next) {
    next()
  },
  beforeRouteLeave(to, from, next) {
    debugger
    console.log(to);
    console.log(from);
    console.log(next);
  }
};
</script>