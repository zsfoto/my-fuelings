<template>
  <f7-page name="details">
    <f7-navbar :title="`${id}`" link="/" back-link="Back"></f7-navbar>

    <f7-block strong>
      <ul>
        <li><b>Main ID:</b> {{mainId}}</li>
        <li><b>ID:</b> {{id}}</li>
        <li><b>Device:</b><br> {{device}}</li>
        <!--li><b>Device:</b> <div v-html="`${device}`"></div></li-->        
      </ul>
	  
	  <f7-list-item title="Vissza" link="/"></f7-list-item>
	  
    </f7-block>
    <f7-block strong>
      <f7-link @click="f7router.back()">Go back via Router API</f7-link>
    </f7-block>
  </f7-page>
</template>
<script>

import { ref, onBeforeMount, onMounted, defineProps } from 'vue';
//import { f7, f7ready } from 'framework7-vue';
import { getDevice }  from 'framework7/lite-bundle';
//import cordovaApp from '../js/cordova-app.js';

export default {
    props: {
      f7route: Object,
      f7router: Object,
    },

	data() {
		return {
			id: null,
			mainId: null,
		}
	},
	
    setup(props) {
		const mainId = ref('')
		const id 	 = ref('')
		const device = getDevice()

		onBeforeMount(() => {
			mainId.value = props.f7route.params.mainId
			id.value 	 = props.f7route.params.id

      console.log(device)

		});

		return {
			device, mainId, id
		}

	},  

	
/*
	mounted() {
		//this.mainId 	= this.f7route.params.mainId;
		//this.id 		= this.f7route.params.id;
	}
*/
	
  };
</script>

