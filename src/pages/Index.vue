<template>
  <f7-page name="main-list">
    <f7-navbar large :sliding="false">
	  <f7-nav-right>
        <f7-link icon-ios="f7:menu" icon-aurora="f7:menu" icon-md="material:menu" panel-open="left" class="nav-link"></f7-link>
      </f7-nav-right>
	  <f7-nav-title sliding>My fuelfills</f7-nav-title>
      <f7-nav-title-large>My fuelfills</f7-nav-title-large>
    </f7-navbar>

    <!--f7-block-title>Lists</f7-block-title-->
    <f7-list>
		<f7-list-item v-for="(i, key) in lists" 
			:key="key" 
			:title="`${i.date}`" 
			:link="`/view/${i.id}/`"
		>{{ i.price }} Ft</f7-list-item>
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
import { ref } from 'vue';

export default {
    props: {
		//f7route: Object,
		f7router: Object,
    },	
	
    setup(props) {
		const lists = ref({});
		
		lists.value = [
			{id: '12006', date: '2022.10.06.', liter: '38,18', price:'15752'},
			{id: '12005', date: '2022.09.30.', liter: '14,68', price:'23752'},
			{id: '12004', date: '2022.09.27.', liter: '22,28', price:'8752'},
			{id: '12003', date: '2022.09.19.', liter: '33,38', price:'12752'},
			{id: '12002', date: '2022.08.13.', liter: '12,48', price:'24752'},
			{id: '12001', date: '2022.08.02.', liter: '32,18', price:'18752'},

		]
		
		
		//const alertLoginData = () => {
			//f7.dialog.alert('Username: ' + username.value + '<br>Password: ' + password.value, () => {
			//	f7.loginScreen.close();
			//});
		//}
		
		
		const Add = () => {
			props.f7router.navigate('/add/')
			//alert('aaa')
		}
		
		
      return {
        lists, Add
      }
	}
}

</script>




