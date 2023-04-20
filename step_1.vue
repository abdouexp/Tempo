<template>

	<div class="step_1" v-auto-animate>
		<h1>هل أنت المالك أو المستأجر؟</h1>
		<div class="row">
			<select class="input100" v-model="inputs.step_1.F1_applicant">
				<option value="">choose ...</option>
				<option value="party_owner">choose this</option>
				<option value="party_tenant">أنا المستأجر</option>
				<option value="party_owner_rep_wa">أنا وكيل الورثة</option>
				<option value="party_owner_rep">أنا الوكيل الشرعي للمالك</option>
				<option value="party_tenant_rep">أنا الوكيل الشرعي للمستأجر</option>
				<option value="waseet">أنا وسيط</option>
				<option value="waseetAssistant">أنا مساعد وسيط</option>
			</select>
		</div>

		<div class="row" v-if="inputs.step_1.F1_applicant == 'waseetAssistant'">
			<input type="text" maxlength="25" placeholder="رقم مساعد الوسيط" v-model="inputs.step_1.F5_waseetAssistantCode" class="input100">
		</div>
		
		<div class="row" v-if="inputs.step_1.F1_applicant == 'party_owner_rep'">
			<select class="input100" v-model="inputs.step_1.F2_ownerRes">
				<option value="">اختر سبب الوكالة</option>
				<option value="waratha">إنشغال المالك الأصلي</option>
				<option value="disabled">المالك عاجز لسبب طبي أو شرعي</option>
				<option value="old">المالك لايعرف للأمور التِقَنية</option>
				<option value="other">أخرى</option>
			</select>
		</div>

		<div class="row" v-if="inputs.step_1.F1_applicant == 'party_tenant_rep'">
			<select class="input100" v-model="inputs.step_1.F3_tenantRes">
				<option value="">اختر سبب الوكالة</option>
				<option value="business">المستأجر منشأة وأنا أمثلها</option>
				<option value="busy">إنشغال المستأجر الأصلي</option>
				<option value="old">المستأجر لايعرف للأمور التِقَنية</option>
				<option value="other">أخرى</option>
			</select>
		</div>

		<div class="row" v-if="inputs.step_1.F1_applicant != ''">
			<select class="input100" v-model="inputs.step_1.F4_suckType">
				<option value="">choose ...</option>
				<option value="digital">choose this</option>
				<option value="old">صك ورقي قديم مكتوب بخط اليد</option>
				<option value="bank">العقار من خلال بنك / شركة</option>

			</select>
		</div>
	</div>

</template>

<script setup>
	import { onMounted , watch , computed} from 'vue'
	import { storeToRefs } from 'pinia'
	import { useOrdersStore } from '@/stores/orders'
	
	const store = useOrdersStore()
	const { url , steps , order , inputs , pricing } = storeToRefs(store)

	watch(() => store.inputs.step_1.F1_applicant , (n) => {
		if(n == 'party_owner_rep_wa' || n == 'party_owner_rep') store.pricing.wakala = 70
		else store.pricing.wakala = 0
	})

	watch(() => store.inputs.step_1.F4_suckType , (n) => {
		if(n == 'old') store.pricing.oldSuck = 28
		else store.pricing.oldSuck = 0
	})


	watch(() => store.pricing , (n) => {
		console.log(n.total)
	})


</script>