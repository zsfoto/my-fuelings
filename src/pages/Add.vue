<template>
<f7-page name="signin">
    <f7-navbar back-link="Back" title="Add fuel fill"></f7-navbar>

    <div class="card">
        <div class="card-header">Add fuel fill</div>
        <div class="card-content">

            <div class="list">
                <ul>

                    <!--li class="item-content item-input">
                        <div class="item-inner">
                            <div class="item-title item-floating-label">Km. óra állása</div>
                            <div class="item-input-wrap">
                                <input type="number" v-model="auto_total_km" autofocus="autofocus" />
                                <span class="input-clear-button"></span>
                            </div>
                        </div>
                    </li-->
                    <li class="item-content item-input">
                        <div class="item-inner">
                            <div class="item-title item-floating-label">Megtett Km.</div>
                            <div class="item-input-wrap">
                                <input type="number" v-model="auto_total_km" />
                                <span class="input-clear-button"></span>
                            </div>
                        </div>
                        <div class="item-inner">
                            <div class="item-title item-floating-label">Napi Km.</div>
                            <div class="item-input-wrap">
                                <input type="number" v-model="auto_trip_km" />
                                <span class="input-clear-button"></span>
                            </div>
                        </div>
                    </li>
					
                    <li class="item-content item-input">
                        <div class="item-inner">
                            <div class="item-title item-floating-label">Fogy. üzema.</div>
                            <div class="item-input-wrap">
                                <input type="number" v-model="auto_fuel_used" />
                                <span class="input-clear-button"></span>
                            </div>
                        </div>
                    <!--/li>
                    <li class="item-content item-input"-->
                        <div class="item-inner">
                            <div class="item-title item-floating-label">Átlagos fogy.</div>
                            <div class="item-input-wrap">
                                <input type="number" v-model="auto_average_consumption" />
                                <span class="input-clear-button"></span>
                            </div>
                        </div>
                    </li>

                    <li class="item-content item-input">
                        <div class="item-inner">
                            <div class="item-title item-floating-label">Benzínkút</div>
                            <div class="item-input-wrap">
                                <input type="text" v-model="which_gas_station" />
                                <span class="input-clear-button"></span>
                            </div>
                        </div>
                    </li>
                    <li class="item-content item-input">
                        <div class="item-inner">
                            <div class="item-title item-floating-label">Üzemanyag típusa</div>
                            <div class="item-input-wrap">
                                <input type="text" v-model="petrol_type" />
                                <span class="input-clear-button"></span>
                            </div>
                        </div>
                    <!--/li>
                    <li class="item-content item-input"-->
                        <div class="item-inner">
                            <div class="item-title item-floating-label">Tankolt liter</div>
                            <div class="item-input-wrap">
                                <input type="number" v-model="petrol_station_filled_liter" />
                                <span class="input-clear-button"></span>
                            </div>
                        </div>
                    </li>

                    <li class="item-content item-input">
                        <div class="item-inner">
                            <div class="item-title item-floating-label">Egységár</div>
                            <div class="item-input-wrap">
                                <input type="number" v-model="petrol_station_unit_price" />
                                <span class="input-clear-button"></span>
                            </div>
                        </div>
                    <!--/li>
                    <li class="item-content item-input"-->
                        <div class="item-inner">
                            <div class="item-title item-floating-label">Kedv.egys.ár</div>
                            <div class="item-input-wrap">
                                <input type="number" v-model="petrol_station_discount_unit_price" />
                                <span class="input-clear-button"></span>
                            </div>
                        </div>
                    </li>
                    <li class="item-content item-input">
                        <div class="item-inner">
                            <div class="item-title item-floating-label">Fizettendő</div>
                            <div class="item-input-wrap">
                                <input type="number" v-model="petrol_station_price" />
                                <span class="input-clear-button"></span>
                            </div>
                        </div>
                    <!--/li>
                    <li class="item-content item-input"-->
                        <div class="item-inner">
                            <div class="item-title item-floating-label">Kedv.végösszeg</div>
                            <div class="item-input-wrap">
                                <input type="number" v-model="petrol_station_discount_price" />
                                <span class="input-clear-button"></span>
                            </div>
                        </div>
                    </li>

                </ul>
            </div>

        </div>
        <div class="card-footer justify-content-center" style="padding-top: 30px;">
            <f7-button class="col color-deeppurple" fill raised @click="SaveFuelfill()">Mentés</f7-button>
        </div>
    </div>

	<br v-for="i in 15">

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
		const auto_fuel_used 						= ref('')
		const auto_total_km 						= ref('')
		const auto_trip_km 							= ref('')
		const auto_average_consumption 				= ref('')
		const petrol_type 							= ref('')
		const petrol_station_filled_liter 			= ref('')
		const petrol_station_price 					= ref('')
		const petrol_station_discount_price 		= ref('')
		const petrol_station_unit_price 			= ref('')
		const petrol_station_discount_unit_price 	= ref('')
		const which_gas_station 					= ref('')

		const details = ref({})
		const device  = getDevice()

		const SaveFuelfill = () => {
			let data = {
				auto_fuel_used: auto_fuel_used.value,
				auto_total_km: auto_total_km.value,
				auto_trip_km: auto_trip_km.value,
				auto_average_consumption: auto_average_consumption.value,
				petrol_type: petrol_type.value,
				petrol_station_filled_liter: petrol_station_filled_liter.value,
				petrol_station_price: petrol_station_price.value,
				petrol_station_discount_price: petrol_station_discount_price.value,
				petrol_station_unit_price: petrol_station_unit_price.value,
				petrol_station_discount_unit_price: petrol_station_discount_unit_price.value,
				which_gas_station: which_gas_station.value
			}
			
			//alert('Adatokat elküldtem a szervernek')
			axios
				.post('http://fueling.vzsfoto.hu/api.php', data)
				.then(response => {
					details.value = response.data
					//props.f7router.navigate('/')
					alert(response)
				})
				.catch(error => {
					console.log(error)
					alert(error)
				})
			
		}
		
/*
		onMounted(() => {		
			//mainId.value = props.f7route.params.mainId
			id.value 	 = props.f7route.params.id

			axios
				.get('http://myf-api.loc/api.php?id=' + id.value)
				//.then(response => (this.info = response))
				.then(response => (details.value = response.data[0]))
				//.then(response => (console.log(response.data)))
				.catch(error => console.log(error))
				// .then(response => (this.info = response.data.bpi))

			//alert(details.value)
		});
*/
		
		// https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/NumberFormat
		// new Intl.NumberFormat('de-DE', { style: 'currency', currency: 'EUR' }).format(number)

		return {
			SaveFuelfill,
			auto_fuel_used, auto_total_km, auto_trip_km, auto_average_consumption,
			petrol_type, petrol_station_filled_liter, petrol_station_price, petrol_station_discount_price, petrol_station_unit_price,
			petrol_station_discount_unit_price, which_gas_station
			
			//device, mainId, id, details
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