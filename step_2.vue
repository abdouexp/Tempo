<template>
	<div class="step_2" v-auto-animate>
		<h1>معلومات المؤجر / المالك</h1>

		<div v-show="inputs.step_1.F1_applicant == 'party_owner'">
			<p class="text-danger text-center">يجب أن يكون المؤجر هو نفسه مالك الصك</p>
			<div class="row">
				<input class="input100" v-model="inputs.step_2.F1_ownerID" dir="ltr" type="text" inputmode="numeric" name="ownerID" pattern="[1-2]{1}[0-9]{9}$" maxlength="10" placeholder="enter 10 digits">
			</div>
			<div class="d-flex justify-content-between">
				<input type="text" dir="ltr" v-model="inputs.step_2.F5_ownerDOB" class="RollDate1 input50" readonly placeholder="click to pick date">
				<input class="input50" v-model="inputs.step_2.F4_ownerMobile" dir="ltr" type="text" name="ownerMobile" inputmode="numeric" maxlength="10" pattern="05[0-9]{8}$" placeholder="enter 10 digits">
			</div>
			<div v-auto-animate>
				<div class="row" v-if="inputs.step_2.ownerCheckupCallback">
					<input type="text" v-model="inputs.step_2.F2_ownerName" class="input100" name="ownerName" placeholder="type your name">
				</div>
				<div class="row" v-if="inputs.step_2.ownerCheckupCallback">
					<input class="input100" v-model="inputs.step_2.F3_ownerIban" dir="ltr" type="text" name="OwnerIban" pattern="^SA[0-9]{22}$" placeholder="رقم حساب آيبان المؤجر لإستلام الايجار">
				</div>
			</div>
		</div>







		<div v-show="inputs.step_1.F1_applicant == 'party_owner_rep_wa'">
			<div class="form-group my-3">
				<div class="d-flex justify-content-between">
					<input class="input50" dir="ltr" v-model="inputs.step_2.F1_ownerID" type="text" inputmode="numeric" pattern="[1-2]{1}[0-9]{9}$" maxlength="10" placeholder="رقم هوية المتوفي" data-type="المؤجر">
					<input class="input50 RollDate2" v-model="inputs.step_2.F5_ownerDOB" dir="ltr" type="text" readonly placeholder="تاريخ ميلاد المتوفي">
				</div>
				<div class="row">
					<input type="text" v-model="inputs.step_2.F2_ownerName" class="input100" disabled placeholder="الاسم الثلاثي للمتوفى صاحب الصك">
				</div>
				<div class="my-4 text-center">معلومات الوكيل الشرعي للورثة</div>
			</div>


			<div class="row">
				<input type="text" v-model="inputs.step_2.F6_ownerRepID" maxlength="25" placeholder="رقم هوية الوكيل الشرعي" class="input100">
			</div>
				
			<div v-auto-animate>
				<div class="d-flex justify-content-between">
					<input class="input50 RollDate3" v-model="inputs.step_2.F9_ownerRepDOB" dir="ltr" type="text" readonly placeholder="تاريخ ميلاد الوكيل">
					<input class="input50" v-model="inputs.step_2.F7_ownerRepMobile" dir="ltr" type="text" inputmode="numeric" maxlength="10" pattern="05[0-9]{8}$" placeholder="رقم جوال الوكيل">
				</div>
				<div class="row">
					<input type="text" v-model="inputs.step_2.F6_ownerRepName" class="input100" @change="store.ArabicOnly" placeholder="الاسم الثلاثي للوكيل الشرعي">
				</div>
				<div class="row">
					<input dir="ltr" type="text" v-model="inputs.step_2.F9_ownerRepIban" pattern="^SA[0-9]{22}$" class="input100" placeholder="رقم حساب الآيبان للوكيل لإستلام الايجار">
				</div>
				<div class="col-md-12 mb-3">
					<input dir="ltr" type="text" class="input100" v-model="inputs.step_2.F10_ownerRepWakalaNumber" inputmode="numeric" placeholder="رقم الوكالة">
				</div>			
			</div>
		</div>






		<div v-show="inputs.step_1.F1_applicant == 'party_owner_rep'">
			<div class="form-group mb-0">
				<div class="d-flex justify-content-between">
					<input class="input50" dir="ltr" v-model="inputs.step_2.F1_ownerID" type="text" inputmode="numeric" pattern="[1-2]{1}[0-9]{9}$" maxlength="10" placeholder="رقم هوية المالك" data-type="المؤجر">
					<input class="input50 RollDate4" v-model="inputs.step_2.F5_ownerDOB" dir="ltr" type="text" readonly placeholder="تاريخ ميلاد المالك">
				</div>
				<div class="row" v-if="inputs.step_2.F1_ownerID.length == 10 && inputs.step_2.F5_ownerDOB.length == 10">
					<div v-if="inputs.step_2.ownerCheckupCallback == 'loading'" class="input100 text-center"><i class="fa fa-refresh fa-spin mt-2"></i></div>
					<input v-if="inputs.step_2.ownerCheckupCallback != 'loading'" type="text" v-model="inputs.step_2.F2_ownerName" class="input100" :disabled="inputs.step_2.ownerCheckupCallback == 'found'" placeholder="الاسم الثلاثي لمالك الصك">
				</div>
			</div>

				
			<div v-auto-animate>

				<div class="my-4 text-center" v-if="inputs.step_2.F2_ownerName.length > 5">معلومات الوكيل الشرعي</div>


				<div class="row" v-if="inputs.step_2.F2_ownerName.length > 5">
					<input type="text" v-model="inputs.step_2.F6_ownerRepID" maxlength="10" placeholder="رقم هوية الوكيل الشرعي" class="input100">
				</div>
				<div class="d-flex justify-content-between" v-if="inputs.step_2.F6_ownerRepID.length == 10">
					<input class="input50" v-model="inputs.step_2.F8_ownerRepMobile" dir="ltr" type="text" inputmode="numeric" maxlength="10" pattern="05[0-9]{8}$" placeholder="رقم جوال الوكيل">
					<input class="input50 RollDate5" v-model="inputs.step_2.F9_ownerRepDOB" type="text" readonly placeholder="تاريخ ميلاده">
				</div>
				<div class="row" v-if="inputs.step_2.checkupCallback == 'failed'">
					<input type="text" v-model="inputs.step_2.F7_ownerRepName" class="input100" @change="store.ArabicOnly" placeholder="الاسم الثلاثي للوكيل الشرعي">
				</div>				
				<div class="row">
					<input dir="ltr" type="text" v-model="inputs.step_2.F10_ownerRepIban" @input="validate_iban" maxlength="24" pattern="^SA[0-9]{22}$" class="input100" placeholder="رقم حساب الآيبان للوكيل لإستلام الايجار">
				</div>
				<div class="col-md-12 mb-3">
					<input dir="ltr" type="text" class="input100" v-model="inputs.step_2.F11_ownerRepWakalaNumber" inputmode="numeric" placeholder="رقم الوكالة">
				</div>			
			</div>
		</div>		
	</div>
</template>

<script setup>
	import { onMounted } from 'vue'
	import { storeToRefs } from 'pinia'
	import Rolldate from 'rolldate-full'
	import { useOrdersStore } from '@/stores/orders'
	
	const store = useOrdersStore()
	const { url , steps , order , inputs } = storeToRefs(store)


	onMounted(() => {
		window.onload = function() {
			new Rolldate({
				el:'.RollDate1',
				format: 'YYYY-MM-DD',
				beginYear: 1350,
				endYear: 1444,
				value: '1375-07-01',
				confirm: function(date) {
					store.inputs.step_2.F5_ownerDOB = date
				}
			})
			new Rolldate({
				el:'.RollDate2',
				format: 'YYYY-MM-DD',
				beginYear: 1350,
				endYear: 1444,
				value: '1375-07-01',
				confirm: function(date) {
					store.inputs.step_2.F5_ownerDOB = date
				}
			})
			new Rolldate({
				el:'.RollDate3',
				format: 'YYYY-MM-DD',
				beginYear: 1350,
				endYear: 1444,
				value: '1375-07-01',
				confirm: function(date) {
					store.inputs.step_2.F9_ownerRepDOB = date
				}
			})
			new Rolldate({
				el:'.RollDate4',
				format: 'YYYY-MM-DD',
				beginYear: 1350,
				endYear: 1444,
				value: '1375-07-01',
				confirm: function(date) {
					store.inputs.step_2.F5_ownerDOB = date
				}
			})
			new Rolldate({
				el:'.RollDate5',
				format: 'YYYY-MM-DD',
				beginYear: 1350,
				endYear: 1444,
				value: '1375-07-01',
				confirm: function(date) {
					store.inputs.step_2.F9_ownerRepDOB = date
				}
			})
			let daDate = new Date();
			let agd18 = Math.floor(Math.floor(Number(daDate.getFullYear()) - Number(622)) * Number(1.031688))-18
			new Rolldate({
				el:'.RollDate6',
				format: 'YYYY-MM-DD',
				beginYear: 1350,
				endYear: agd18,
				value: '1405-06-15',
				confirm: function(date) {
					return checkAgeH(date);
				}
			})
			new Rolldate({
				el:'.RollDate7',
				format: 'YYYY-MM-DD',
				beginYear: 2022,
				endYear: 2025,
				confirm: function(date) {
					store.inputs.step_5.F4_contractStartDate = date
				}
			})

		}
	})


	
	function validate_iban(){
		store.inputs.step_2.ibanValidation = '---'
		let iban = store.inputs.step_2.F10_ownerRepIban
		// if(iban.lingth != 24) return false

		var letter = new Array ("A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M","N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z");
		var digits = new Array ("10","11","12","13","14","15","16","17","18","19","20","21","22","23","24","25","26","27","28","29","30","31","32","33","34","35");
		var sa_ilen = 24;
		var sa_bban = /\d{2}[A-Za-z0-9]{18}/;
		let pattern = /\W|_/;
		if (pattern.test(iban)){store.inputs.step_2.ibanValidation = 'E1'}
		pattern = /^\D\D\d\d.+/;
		if (pattern.test(iban) == false){store.inputs.step_2.ibanValidation = 'E2'}
		pattern = /^\D\D00.+|^\D\D01.+|^\D\D99.+/;
		if (pattern.test(iban)){store.inputs.step_2.ibanValidation = 'E3'}
		let ctry = iban.substr(0, 2);
		if (ctry != 'SA') {store.inputs.step_2.ibanValidation = 'E4'}
		if ((iban.length - sa_ilen) != 0){store.inputs.step_2.ibanValidation = 'E5'}
		pattern = sa_bban;
		if (pattern.test(iban.substr(4, sa_ilen - 4)) == false){store.inputs.step_2.ibanValidation = 'E6'}
		iban = iban.toUpperCase();
		iban = iban.substr(4, sa_ilen - 4) + iban.substr(0, 4);
		let i
		for (i = 0; i <= 25; i++)
		{
			while (iban.search(letter[i])!= -1)
			{
				iban = iban.replace(letter[i], digits[i]);
			}
		}
		let coss = Math.ceil(iban.length / 7);
		let rmndr = "";
		for (i = 1; i <= coss; i++){rmndr = String(parseFloat(rmndr + iban.substr((i - 1) * 7, 7)) % 97);}
		if (rmndr != "1"){ store.inputs.step_2.ibanValidation = 'E7';} 
		store.inputs.step_2.ibanValidation = 'ok';
	}


	function checkAgeH(DOB) {
		var daDate = new Date()
		var str= DOB.split('-')
		if(Math.floor(Math.floor(Number(daDate.getFullYear()) - Number(622)) * Number(1.031688))-18 <= str[0]){
			Swal.fire({
				html: "حسب توجيهات وزارة الإسكان ، يجب أن يكون عمر المستأجر أكبر من 18 سنة",
				showConfirmButton: true,
				confirmButtonText: 'اوكي',
				icon:'error',
				width:330,
			})
			return false;
		}
		store.inputs.step_3.F4_tenantDOB = DOB
		return DOB;
	}
</script>