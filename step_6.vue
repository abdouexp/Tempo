<template>
	<div class="step_3">
		<h1>العنوان الوطني</h1>
		
		<p class="addressExplain">كأحد متطلبات العقد وبناء على توجيهات وزارة الاسكان زودنا بالعنوان الوطني للمبنى أو حدد مكانه على الخريطة</p>
		
		<div class="choseAdress">
			<div :class="{active : inputs.step_6.F1_addressType == 'manual'}" @click="inputs.step_6.F1_addressType = 'manual'"> 
				<img v-if="inputs.step_6.F1_addressType == ''" src="https://s.agd.sa/img/nAdress.png" alt="">
				<p>إدخال يدوي</p>
			</div>
			<div :class="{active : inputs.step_6.F1_addressType == 'map'}" @click="inputs.step_6.F1_addressType = 'map'">
				<img v-if="inputs.step_6.F1_addressType == ''" src="https://s.agd.sa/img/onMap.png" alt="">
				<p>choose this</p>
			</div>
		</div>



		


		<div v-show="inputs.step_6.F1_addressType == 'manual'" class="overflow-hidden">
			<hr class="my-3">
			<div class="row">
				<select class="input100" v-model="inputs.step_6.F4_area">
					<option :value="id" :key="id" v-for="(region,id) in regions">{{ region }}</option>
				</select>			
			</div>
			<div class="d-flex justify-content-between mb-3">
				<!-- <input type="text" class="input50 me-15" placeholder="المدينة"> -->
				<div v-if="loadCities" class="input50 text-center"><i class="fa fa-refresh fa-spin mt-2"></i></div>
				<Dropdown v-if="!loadCities && steps.current == 6" v-model="inputs.step_6.F5_city" :options="cities" optionLabel="name_ar" optionValue="id" emptyFilterMessage="لاتوجد نتيجة" emptyMessage="اختر المنطقة لعرض مدنها" :filter="true" filterIcon="fa-solid fa-search" placeholder="اختر المدينة" class="input50 me-15" />
				<input type="text" class="input50" dir="ltr" v-model="inputs.step_6.F6_buliding" inputmode="numeric" maxlength="5" placeholder="رقم المبنى" name="building_number">
			</div>
			<div class="d-flex justify-content-between">
				<input type="text" class="input50" dir="ltr" v-model="inputs.step_6.F7_postal" inputmode="numeric" maxlength="5" placeholder="الرمز البريدي" name="postal">
				<input type="text" class="input50" dir="ltr" v-model="inputs.step_6.F8_additional" inputmode="numeric" maxlength="5" placeholder="الرقم الإضافي" name="additional">
			</div>
		</div>
		
		<div v-show="inputs.step_6.F1_addressType == 'map'" id="map" class="mt-3"></div>
		<input type="hidden" id="loc" @click="getLoc">

	</div>
</template>

<script setup>
	import Dropdown from 'primevue/dropdown'
	import { watch , ref, onMounted } from 'vue'
	import { storeToRefs } from 'pinia'
	import { useOrdersStore } from '@/stores/orders'
	
	const store = useOrdersStore()
	const { url , steps , order , inputs } = storeToRefs(store)
	
	const regions =  ['اختر المنطقة','الرياض','مكة المكرمة','المدينة المنورة','المنطقة الشرقية','القصيم','حائل','عسير','جازان','الباحة','نجران','تبوك','الحدود الشمالية','الجوف']
	let cities = ref({})
	let loc = ref('')
	let loadCities = ref(false)



	const get_cities = (async (id) => {
		loadCities.value = true;
		axios.post(store.url+'get/cities/'+id+'?get-cities').then(response => {
			loadCities.value = false;
			cities  = response.data
		})
	})

	let getLoc = ((event) => {
		if(event.target.value != ''){
			let loc = event.target.value.split(',')
			store.inputs.step_6.F2_lat = Number(loc[0])
			store.inputs.step_6.F3_lon = Number(loc[1])
		}

	})

</script>