<template>
  <f7-page name="details">
    <!--f7-navbar :title="`${details.created.replaceAll('-','.')}`" link="/" back-link="Back"></f7-navbar-->
    <f7-navbar :title="`${details.created}`" link="/" back-link="Back"></f7-navbar>

    <f7-block strong>

	  <h3><b>Mentett adatok</b></h3>
	  <table width="100%" border="1" cellpadding="2" cellspacing="0">
		<tr><td width="50%">id:</td><td><b>{{ details.id }}</b></td></tr>
		<tr><td>Megtett össz. km:</td><td><b>{{ details.auto_total_km }}</b> km.</td></tr>
		<tr><td>Elfogyasztott üzemeanyag:</td><td><b>{{ details.auto_fuel_used }}</b> l</td></tr>
		<tr><td>Napi km:</td><td><b>{{ details.auto_trip_km }}</b>  km.</td></tr>
		<tr><td>Átlagos fogyasztás:</td><td><b>{{ details.auto_average_consumption }}</b> l/100km</td></tr>
		<tr><td>Üzemanyag típusa:</td><td><b>{{ details.petrol_type }}</b></td></tr>
		<tr><td>Tankolt üzemanyag:</td><td><b>{{ details.petrol_station_filled_liter }}</b> liter</td></tr>
		<tr><td>Fizetendő:</td><td><b>{{ details.petrol_station_price }}</b> Ft</td></tr>
		<tr><td>Ársapkás ár:</td><td><b>{{ details.petrol_station_discount_price }}</b> Ft</td></tr>
		<tr><td>Egységár:</td><td><b>{{ details.petrol_station_unit_price }}</b> Ft</td></tr>
		<tr><td>Ársapkás egységár:</td><td><b>{{ details.petrol_station_discount_unit_price }}</b>Ft</td></tr>
		<tr><td>Melyik benzinkút:</td><td><b>{{ details.which_gas_station }}</b></td></tr>
		<tr><td>GPS:</td><td>Long: <b>{{ details.gps_long }} </b>/ Lat: <b>{{ details.gps_lat }}</b></td></tr>
	  </table>

        <!--li><b>Main ID:</b> {{mainId}}</li>
        <li><b>ID:</b> {{id}}</li>
        <li><b>Device:</b><br> {{device}}</li-->
        <!--li><b>Device:</b> <div v-html="`${device}`"></div></li-->
		
      <!--ul>
		<li>id: <b>{{ details.id }}</b></li>
		<li>Elfogyasztott üzemeanyag: <b>{{ details.auto_fuel_used }}</b></li>
		<li>Megtett össz. km: <b>{{ details.auto_total_km }}</b></li>
		<li>Napi km: <b>{{ details.auto_trip_km }}</b></li>
		<li>Átlagos fogyasztás: <b>{{ details.auto_average_consumption }}</b></li>
		<li>Tankolt üzemanyag: <b>{{ details.petrol_station_filled_liter }}</b></li>
		<li>Fizetendő: <b>{{ details.petrol_station_price }}</b></li>
		<li>Ársapkás ár: <b>{{ details.petrol_station_discount_price }}</b></li>
		<li>Egységár: <b>{{ details.petrol_station_unit_price }}</b></li>
		<li>Ársapkás egységár: <b>{{ details.petrol_station_discount_unit_price }}</b></li>
		<li>Melyik benzinkút: <b>{{ details.which_gas_station }}</b></li>
		<li>Üzemanyag típusa: <b>{{ details.petrol_type }}</b></li>
		<li>GPS: <b>{{ details.gps_long }} / {{ details.gps_lat }}</b></li>
		<li>Dátum, idő: <b>{{ details.created }}</b></li>		
	  
      </ul-->
	  
	  <!--f7-link link="/">Vissza a főoldalra</f7-link-->
	  
    </f7-block>
    
	<!--f7-block strong>
      <f7-link @click="f7router.back()">Go back via Router API</f7-link>
    </f7-block-->
	
  </f7-page>
</template>

<script>
import { ref, onBeforeMount, onMounted, defineProps } from 'vue';
//import { f7, f7ready } from 'framework7-vue';
import { getDevice }  from 'framework7/lite-bundle';
//import cordovaApp from '../js/cordova-app.js';
import axios from 'axios';

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
		const details= ref({})
		const device = getDevice()

		onBeforeMount(() => {
			mainId.value = props.f7route.params.mainId
			id.value 	 = props.f7route.params.id

/*
			axios
				.get('http://myf-api.loc/api.php?id=' + id.value)
				//.then(response => (this.info = response))
				.then(response => (details.value = response.data))
				//.then(response => (console.log(response.data)))
				.catch(error => console.log(error))				
				// .then(response => (this.info = response.data.bpi))
*/

			//console.log(device)

		});
		
		onMounted(() => {		
			//mainId.value = props.f7route.params.mainId
			id.value 	 = props.f7route.params.id

			axios
				.get('http://fueling.vzsfoto.hu/api.php?id=' + id.value)
				//.then(response => (this.info = response))
				.then(response => (details.value = response.data[0]))
				//.then(response => (console.log(response.data)))
				.catch(error => console.log(error))
				// .then(response => (this.info = response.data.bpi))

			//alert(details.value)
			
			//console.log('det')
			//console.log(details.value)
			//console.log('--det')


		});
		
		// https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/NumberFormat
		// new Intl.NumberFormat('de-DE', { style: 'currency', currency: 'EUR' }).format(number)

		return {
			device, mainId, id, details
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

<style>
	table, td {
		border: 1px solid lightgray;
	}
</style>