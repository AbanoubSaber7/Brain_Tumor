<template>
  <div class="services container">
    <div class="row text-center">
      <h1>
        Scan Now!
      </h1>
      
    </div>
    <div class="row align-items-center">
      <!-- <div class="col-lg-6 col-sm-12">
        <div class="image">
          <img src="../../assets/serv.png" alt="">
        </div>
      </div> -->
      <Secvices :userid="state.userid" />
      <Secvices2 :userid="state.userid" />
      
      
    </div>
  </div>
  <Doctor class="mt-5"></Doctor>
</template>

<script>
import { onMounted, reactive } from "vue";
import axios from "axios";
import { useStore } from "vuex";
import { useRouter } from "vue-router";
import Secvices from '../../components/Services/Secvices.vue'
import Secvices2 from '../../components/Services/Secvices2.vue'
import Doctor from "@/components/Doctor/Doctor.vue";
export default {
  components:{
    Secvices,
    Doctor,
    Secvices2
  },
  setup() {
    const state = reactive({
      image: "",
      userid:''
    });
    const store = useStore();
    const router = useRouter();
    onMounted(() => {
      const token = localStorage.getItem("token");
      if (store.state.patient == null || !token) {
        router.push("/login");
        return;
      }
      state.userid = store.state.patient.id;
      if (token) {
        axios.defaults.headers.common["Authorization"] = `Bearer ${token}`;
      }
    });
    
    return { state,store };
  },
};
</script>

<style lang="scss">
.services{
  margin-top: 80px;
  // align-items: center;
  h1{
    color: var(--textcolor);
    font-weight: 600;
    margin-top: 10px;
  }
  img{
    width: 80%;
  }
}
</style>