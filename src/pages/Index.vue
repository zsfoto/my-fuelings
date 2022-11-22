<template>
  <f7-page name="main-list">
    <f7-navbar large :sliding="false">
	  <f7-nav-right>
        <f7-link icon-ios="f7:menu" icon-aurora="f7:menu" icon-md="material:menu" panel-open="left" class="nav-link"></f7-link>
      </f7-nav-right>
	  <f7-nav-title sliding>My fuelings</f7-nav-title>
      <f7-nav-title-large>My fuelings</f7-nav-title-large>
    </f7-navbar>

    <!--f7-block-title>Lists</f7-block-title-->
	
    <f7-list>
		<f7-list-item v-for="(i, key) in list" 
			:key="key" 
			:title="`${i.created.substring(0, 10).replaceAll('-','.')}.`"
			:link="`/view/${i.id}/`"
		>{{ i.petrol_station_filled_liter }} liter • {{ i.petrol_station_discount_price.toLocaleString('hu-HU') }} Ft</f7-list-item>
    </f7-list>

	<div class="fab fab-extended fab-right-bottom color-red" @click="Add">
		<a href="#">
			<i class="icon f7-icons if-not-md">plus</i>
			<i class="icon material-icons md-only">add</i>
			<!--div class="fab-text">Create</div-->
		</a>
	</div>
 
  </f7-page>
</template>


<script>
import { ref, onMounted } from 'vue';
//import { f7, f7ready } from 'framework7-vue';
import axios from 'axios';

export default {
    props: {
		//f7route: Object,
		f7router: Object,
    },	
	
    setup(props) {
		const list = ref({});

		onMounted(() => {
		
			axios
				.get('http://fueling.vzsfoto.hu/api.php')
				.then(response => (list.value = response.data))
					.catch(error => console.log(error))				

			//console.log(list.value)

			//f7.dialog.alert('aaaa<br>Password', () => {
			//	//f7.loginScreen.close();
			//});

		});
		
		const Add = () => {
			props.f7router.navigate('/add/')
		}
		
		
      return {
        list, Add
      }
	}
}

</script>




