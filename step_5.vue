<template>
	<div class="step_5" v-auto-animate>
		<h1>ادخل بيانات العقد الجديد</h1>








		
		<div class="form-group col-md-12 col-sm-12 col-12 p-0">
			<div class="row">
				<input type="text" dir="ltr" v-model="inputs.step_5.F1_contractAmount" inputmode="numeric" maxlength="6" class="input100" placeholder="enter 4 digits">
			</div>
			<div class="d-flex justify-content-between mb-3">
				<select v-model="inputs.step_5.F3_contractPaymentCycle" class="input50">
					<option value="" selected="">choose ...</option>
					<option value="monthly">choose this</option>
					<option value="quarterly">كل 3 أشهر</option>
					<option value="bi-annual">كل 6 أشهر</option>
					<option value="annual">سنوي</option>
					<option value="one_time_pay">دفعة واحدة</option>
				</select>
				<select v-model="inputs.step_5.F2_contractDuration" class="input50">
					<option value="" selected="">choose ...</option>
					<option value="3-month">choose this</option>
					<option value="6-month">6 شهور</option>
					<option value="1-year">1 سنة</option>
					<option value="2-year">سنتين</option>
					<option value="3-year">3 سنوات</option>
					<option value="4-year">4 سنوات</option>
					<option value="5-year">5 سنوات</option>
					<option value="6-year">6 سنوات</option>
					<option value="7-year">7 سنوات</option>
					<option value="8-year">8 سنوات</option>
					<option value="9-year">9 سنوات</option>
					<option value="10-year">10 سنوات</option>
				</select>			
			</div>
			<div class="row mb-3">
					<select class="input100" v-model="inputs.step_5.F5_unitType" @change="toggleRest">
						<option value="" selected>choose ...</option>
						<option value="apartment">choose this</option>
						<option value="studio">شقَّة صغيرة (استوديو)</option>
						<option value="drivers_room">غرفة سائق</option>
						<option value="floor">دور</option>
						<option value="villa">فيلا</option>
						<option value="building">عمارة</option>
						<option value="tower">برج</option>
						<option value="duplex">شقة ثنائية الدور (دوبلكس)</option>
						<option value="penthouse_villa">فيلا روف</option>
						<option value="secondary_apartment">ملحق علوي</option>
						<option value="apartment_extension">شقة + ملحق علوي</option>
						<option value="floor_extension">دور + ملحق علوي</option>
						<option value="other">اخرى</option>
					</select>			
			</div>
			<div class="showRest" style="display: none">
				<div class="row mt-0">
					<input type="text" dir="ltr" v-model="inputs.step_5.F21_unitArea" inputmode="numeric" maxlength="6" class="input100" placeholder="enter 2 digits">
				</div>					
				<div class="d-flex justify-content-between mb-3">
					<input type="text" class="input50 RollDate7" v-model="inputs.step_5.F4_contractStartDate" placeholder="click to pick date" readonly>
					<input type="text" class="input50" dir="ltr" v-model="inputs.step_5.F6_unitFloor" inputmode="numeric" maxlength="2" placeholder="enter 1 digits">
				</div>
				
				<div class="d-flex justify-content-between mb-3">
					<input type="text" dir="ltr" inputmode="numeric" v-model="inputs.step_5.F7_unitNumber" maxlength="4" class="input50" placeholder="enter 1 digits">	
					<input type="text" dir="ltr" inputmode="numeric" v-model="inputs.step_5.F8_unitRooms" maxlength="2" class="input50" placeholder="enter 1 digits">
				</div>

				<div class="btn btn-primary w-100" role="button" @click="toggleOptions">{{ moreOptText }}</div>

				<div class="moreOptShow" style="display: none">
					<div class="row mb-4">
						<div class="col-12 pe-0">
							<div class="form-checkform-check form-switch ps-0 pe-1 text-start">
								<label class="form-check-label" for="SW01">حوض المطبخ راكب</label>
								<input class="form-check-input float-end me-2" v-model="inputs.step_5.F11_unitKetchenSync" type="checkbox" role="switch" id="SW01" true-value="1" false-value="0">
							</div>
						</div>
					</div>

					<div class="row mb-4">
						<div class="col-12 pe-0">
							<div class="form-checkform-check form-switch ps-0 pe-1 text-start">
								<label class="form-check-label" for="SW02">دواليب المطبخ راكبة</label>
								<input class="form-check-input float-end me-2" v-model="inputs.step_5.F12_unitKetchenCabinets" type="checkbox" role="switch" id="SW02" true-value="1" false-value="0">
							</div>
						</div>
					</div>

					<div class="row mb-4">
						<div class="col-12 pe-0">
							<div class="form-checkform-check form-switch ps-0 pe-1 text-start">
								<label class="form-check-label" for="SW04">يوجد غرفة للخادمة</label>
								<input class="form-check-input float-end me-2" v-model="inputs.step_5.F17_unitMeadRoom" type="checkbox" role="switch" id="SW04" true-value="1" false-value="0">
							</div>
						</div>
					</div>

					<div class="row mb-4">
						<div class="col-12 pe-0">
							<div class="form-checkform-check form-switch ps-0 pe-1 text-start">
								<label class="form-check-label" for="SW05">يوجد غرفة مخزن</label>
								<input class="form-check-input float-end me-2" v-model="inputs.step_5.F16_unitStoreRoom" type="checkbox" role="switch" id="SW05" true-value="1" false-value="0">
							</div>
						</div>
					</div>

					<div class="d-flex justify-content-between mb-3">
						<input type="text" dir="ltr" inputmode="numeric" v-model="inputs.step_5.F13_unitWindowAC" class="input50" maxlength="12" placeholder="مكيفات شباك">	
						<input type="text" dir="ltr" inputmode="numeric" v-model="inputs.step_5.F15_unitSplitAC" class="input50" maxlength="12" placeholder="مكيفات سبليت">
					</div>

					<div class="d-flex justify-content-between mb-3">
						<input type="text" dir="ltr" inputmode="numeric" v-model="inputs.step_5.F18_unitElectricityMeter" class="input50" maxlength="12" placeholder="رقم عداد الكهربة">	
						<input type="text" dir="ltr" inputmode="numeric" v-model="inputs.step_5.F18_unitWaterMeter" class="input50" maxlength="12" placeholder="رقم عداد الموية">
					</div>

					<div class="d-flex justify-content-between mb-3">
						<input type="text" dir="ltr" inputmode="numeric" v-model="inputs.step_5.F9_unitInsurance" class="input50" maxlength="12" placeholder="مبلغ التأمين">
						<input type="text" dir="ltr" inputmode="numeric" v-model="inputs.step_5.F10_unitPenalty" class="input50" maxlength="12" placeholder="مبلغ الغرامة اليومي">	
					</div>
				</div>
			</div>
		</div>



	</div>
	
</template>

<script setup>
	import { onMounted , toRefs , ref} from 'vue'
	import { storeToRefs } from 'pinia'
	import { useOrdersStore } from '@/stores/orders'
	
	const store = useOrdersStore()
	const { url , steps , order , inputs } = storeToRefs(store)
	let showRest = ref(false)
	let moreOptShow = ref(false)
	let moreOptText = ref('اضغط هنا لعرض المزيد من الخيارات')

	const toggleOptions = ( () => {
		if(moreOptShow.value){
			moreOptShow.value = false
			store.inputs.step_5.F20_moreOptions = 'off'
			moreOptText.value = 'اضغط هنا لعرض المزيد من الخيارات'
			// $('.moreOptShow').slideUp(750)
		}else{
			moreOptShow.value = true
			store.inputs.step_5.F20_moreOptions = 'on'
			moreOptText.value = 'إخفاء الخيارات الأختيارية'
			// $('.moreOptShow').slideDown(750)
		}
	});

	const toggleRest = ( () => {
		if(store.inputs.step_5.F5_unitType == ''){
			showRest.value = false
			moreOptShow.value = false
			// $('.showRest').slideUp(750)
		}else{
			showRest.value = true
			// $('.showRest').slideDown(750)
		}
	});

</script>