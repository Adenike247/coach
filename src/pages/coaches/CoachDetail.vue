<template>
  <section>
    <base-card>
    <h2>{{ fullName}}</h2>
    <h3>${{ rate}}/hour</h3>
  </base-card>
  </section>
  <section>
    <base-card>
    <header>
      <h2>Interested? Reach out now!</h2>
    <base-button link :to="contactlink">Contaact</base-button>
    </header>
    <router-view></router-view>
  </base-card>
  </section>
  <section>
    <base-card>
    <basebadge v-for="area in areas" :key="area" :type="area" :title="area"></basebadge>
    <p>{{description}}</p>
  </base-card>
  </section>
</template>

<script>
export default {
  props:['id'],
  data() {
    return {
      selectedCoach: null
    };
  },
  computed:{
    fullName() {
      return this.selectedCoach.firstName + '' + this.selectedCoach.lastName;

    },
    areas(){
      return this.selectedCoach.areas;
    },
    rate() {
      return this.selectedCoach.hourlyRate;
    },
    descriptions(){
      return this.selectedCoach.description;
    },
    contactLink() {
      return this.$router.path + '/' + this.id + '/contact';
    }
  },
  created() {
    this.selectedCoach = this.$store.getters['coaches/coaches'].
    find((coach) => coach.id);
    
  },
};
</script>