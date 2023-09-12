<script >
export default {
  name: 'home',
  data(){
    return {
      studetns_count: 0,
      teaching_count: 0,
      final_count: 0,
      groups_count: 0,
      money_count: 0,
      plans_count: 0
    }
  }
}
</script>

<template>
  <div class="container">
    <div class="row">
      <div class="col" style="background-color: rgba(0, 255, 255, 0.199);">
        <h4>Markaz umumiy o'quvchilari soni</h4>
        <p>
          {{studetns_count}}
        </p>
      </div>
      <div class="col" style="background-color: rgba(230, 81, 81, 0.616);">
        <h4>O'qiyotgan o'quvchilar soni</h4>
        <p>{{teaching_count}}</p>
      </div>
      <div class="col" style="background-color: rgba(0, 128, 0, 0.445);">
        <h4>O'qishni bitirgan o'quvchilar soni</h4>
        <p>{{ final_count }}</p>
      </div>
      <div class="col" style="background-color: rgba(250, 128, 114, 0.637);">
        <h4>O'quv kurslari soni</h4>
        <p>{{groups_count}}</p>
      </div>
      <div class="col" style="background-color: rgba(255, 255, 0, 0.336);">
        <h4>Tushumlar miqdori</h4>
        <p>{{money_count}}</p>
      </div>
      <div class="col">
        <h4>Rejalar soni</h4>
        <p>{{plans_count}}</p>
      </div>
    </div>
  </div>
</template>


<style scoped>
  .container{
    width: 80%;
    background-color: rgba(128, 128, 128, 0.048);
  }

  .row{
    display: grid;
    padding: 10px;
    column-gap: 10px;
    grid-template-columns: auto auto auto;
    row-gap: 10px;
  }
  .col{
    display: block;
    min-height: 300px;
    border-radius: 1rem;
    background-color: white;
    margin: 0 10px;
    box-shadow: 0 0 5px rgba(171, 214, 103, 0.733);
  }
  .col h4{
    text-align: center;
  }
  .col p{
    text-align: center;
    padding-top: 30px;
    font-size: 30px;
    font-weight: bold;
  }
</style>
