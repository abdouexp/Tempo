<template>
	<div class="overall" v-if="load"><div class="lds-ripple"><p class="mb-4"></p><div></div><div></div></div></div>
	<div class="all-container">
		<header>
			<div class="branding d-none"></div>
			<div class="steps">
				<div class="step step-1" @click="store.step(1)" :class="{active : steps.current == 1}"><div class="number">1</div><div class="title">البداية</div></div>
				<div class="step step-2" @click="store.step(2)" :class="{active : steps.current == 2}"><div class="number">2</div><div class="title">المالك</div></div>
				<div class="step step-3" @click="store.step(3)" :class="{active : steps.current == 3}"><div class="number">3</div><div class="title">المستأجر</div></div>
				<div class="step step-4" @click="store.step(4)" :class="{active : steps.current == 4}"><div class="number">4</div><div class="title">الصك</div></div>
				<div class="step step-5" @click="store.step(5)" :class="{active : steps.current == 5}"><div class="number">5</div><div class="title">الوحدة</div></div>
				<div class="step step-6" @click="store.step(6)" :class="{active : steps.current == 6}"><div class="number">6</div><div class="title">العنوان</div></div>
			</div>
			<div class="steps-bar"></div>
		</header>
		<div class="content">

			<step_1 v-show="steps.current == 1" />
			<step_2 v-show="steps.current == 2" />
			<step_3 v-show="steps.current == 3" />
			<step_4 v-show="steps.current == 4" />
			<step_5 v-show="steps.current == 5" />
			<step_6 v-show="steps.current == 6" />


			<div class="actions" v-auto-animate>
				<button class="back" v-if="steps.current > 1" @click="store.back"><i class="fa-solid fa-arrow-right-long"></i> back</button>
				<button class="next" v-if="steps.current < 6" @click="store.next">next</button>
				<button class="submit" v-if="steps.current == 6" @click="store.submit">submit</button>
			</div>

		</div>
		<footer>
			<div class="links">
				<a @click="showPrice">تفصيل السعر ({{ pricing.total }} رس)</a>
			</div>
			<div class="copy">جميع الحقوق محفوظة</div>
		</footer>
	</div>

</template>

<script setup>
	import step_1 from './step_1.vue'
	import step_2 from './step_2.vue'
	import step_3 from './step_3.vue'
	import step_4 from './step_4.vue'
	import step_5 from './step_5.vue'
	import step_6 from './step_6.vue'

	import { onMounted , watch } from 'vue'
	import { storeToRefs } from 'pinia'
	import Swal from 'sweetalert2/dist/sweetalert2'
	import { useOrdersStore } from '@/stores/orders'
	

	const store = useOrdersStore()
	const props = defineProps(['id'])
	const { url , steps , order , inputs , pricing , load } = storeToRefs(store)

	const p = window.location.search.slice(1)
	if(p) store.steps.current = p
	else store.steps.current = 1



	onMounted(() => {
		store.load = false
		// setTimeout(()=>{
		// 	getHistory()
		// 	store.inputs.account_id = props.id
		// },2000)
	})





	const showPrice = (() => {
		let wakala = '',oldSuck = ''
		let duration = (store.inputs.F2_contractDuration == null) ? 1:store.inputs.F2_contractDuration
		if(store.pricing.wakala > 0) wakala = '<tr><td class="text-start">معالجة صك وكالة</td><td class="text-end">'+store.pricing.wakala+' رس</td></tr>'
		if(store.pricing.oldSuck > 0) oldSuck = '<tr><td class="text-start">معالجة صك ورقي</td><td class="text-end">'+store.pricing.oldSuck+' رس</td></tr>'
		
		Swal.fire({
			title: 'تفصيل السعر',
			html: 'مدة العقد المختارة هي ('+duration+') سنة<br><br><table dir="rtl" width="100%" class="table" cellspacing="0">'+
				'<tr><td class="text-start">شبكة إيجار الحكومية</td><td class="text-end">'+store.pricing.gov+' رس</td></tr>'+
				'<tr><td class="text-start">رسوم توثيق أبشر وSMS</td><td class="text-end">'+store.pricing.services+' رس</td></tr>'+
				'<tr><td class="text-start">مؤسسة (عقد إيجار)</td><td class="text-end">'+store.pricing.office+' رس</td></tr>'+
				wakala+
				oldSuck+
				'<tr>'+
					'<td class="text-start">ضريبة القيمة المضافة</td><td class="text-end">'+store.pricing.vat+' رس</td>'+
				'</tr><tr>'+
				'<td class="total text-start">المجموع</td><td class="text-end">'+store.pricing.total+' رس</td></tr></table>',
			confirmButtonText: 'تمام',
			width: 330,
		})
	})


	const requirements = (() => {
		Swal.fire({
			title: 'طلبات قبل نبدأ',
			html: '<div class="text-start">'+
				'<p>لخدمتك بشكل سريع ، جهّز التالي:</p><ul>'+
					'<li>معلومات هوية المؤجر والمستأجر</li>'+
					'<li>جوال الطرفين المسجل في ابشر</li>'+
					'<li>رقم الحساب البنكي (آيبان) للمؤجر</li>'+
					'<li>رقم الصك الإلكتروني من المؤجر</li>'+
					'<li>الدور ، عدد الغرف ، عدد أدوار المبنى</li>'+
					'<li>مساحة الوحدة العقارية</li>'+
					'<li>وأخيراً 299 رس رسوم الخدمة</li>'+
					'</ul></div>',
			confirmButtonText: 'تمام',
			width: 330,
		})
	})

	const getHistory = (async () => {
		axios.post(store.url+'get/history/welcome=)').then(response => {
			store.load = false
			
			if(response.data != ''){
				store.inputs = response.data[0]
				store.inputs.order_id = response.data.order_id				
			}else{
				requirements()
			}

		})
	})



</script>