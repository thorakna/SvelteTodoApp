<script>
    import "../app.css";
  </script>
  <main class="container">
    <h2 class=" text-sky-500 font-bold text-2xl mb-5">Onur's Todo List</h2>
    <slot />
  </main>
  
<style>
  .container{
      display:flex;
      flex-direction: column;
      align-items: center;
      max-width: 100vw;
      height: 100vh;
      background: #172241 no-repeat;
      background-size: cover;
      padding-top: 2vh;
      padding-left: 2vw;
      padding-right: 2vw;
  }
</style>