<template>
	<div class="step_3">
		<h1>معلومات المستأجر</h1>
		<input class="input100 mb-3" v-model="inputs.step_3.F1_tenantID" dir="ltr" type="text" name="tenantID" inputmode="numeric" pattern="[1-2]{1}[0-9]{9}$" maxlength="10" placeholder="enter 10 digits">
		<div>
			<div class="row d-none">
				<input type="text" v-model="inputs.step_3.F2_tenantName" class="input100" name="tenantName" placeholder="enter your name">
			</div>
			<div class="d-flex justify-content-between">
				<input class="input50 RollDate6" v-model="inputs.step_3.F4_tenantDOB" type="text" readonly placeholder="click to pick date">
				<input class="input50" v-model="inputs.step_3.F3_tenantMobile" dir="ltr" name="tenantMobile" type="text" inputmode="numeric" pattern="05[0-9]{8}$" maxlength="10" placeholder="enter 10 digits">
			</div>
		</div>
	</div>
</template>

<script setup>
	import { storeToRefs } from 'pinia'
	import { useOrdersStore } from '@/stores/orders'
	
	const store = useOrdersStore()
	const { url , steps , order , inputs } = storeToRefs(store)


</script>