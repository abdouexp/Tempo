<template>
	<div class="step_4">
		<h1>معلومات الصك</h1>

		<div v-if="inputs.step_1.F4_suckType == 'digital'">
			<div class="row">
				<input type="text" v-model="inputs.step_4.F1_suckNumber" dir="ltr" inputmode="numeric" maxlength="12" class="input100" name="suck_number" placeholder="enter 12 digits"/>
			</div>
			<div class="ExplainTawaklna">أضغط هنا لشرح لكيفية الحصول على رقم الصك</div>
			
			<div v-if="inputs.step_4.suckValidation == 'manual'">
				<div class="row">
					<input type="text" v-model="inputs.step_4.F2_suckDate" class="input100 RollDate6" readonly placeholder="تاريخ الصك"/>
				</div>

				<div class="row">
					<select class="input100" v-model="inputs.step_4.F6_propertyType">
						<option value="">حدد نوع العقار</option>
						<option value="building">عمارة</option>
						<option value="villa">فيلا</option>
						<option value="plaza">بلازا</option>
						<option value="shopping_mall">مول</option>
						<option value="tower">برج</option>
						<option value="land">أرض</option>
						<option value="other">أخرى</option>
					</select>
				</div>					
				<div class="d-flex justify-content-between">
						<input type="text" v-model="inputs.step_4.F8_propertyFloors" dir="ltr" inputmode="numeric" maxlength="2" class="input50 me-15" placeholder="عدد أدوار المبنى"/>
						<select class="input50 ms-15" v-model="inputs.step_4.F7_propertyUse">
							<option value="">استخدام المبنى</option>
							<option value="residential_families">سكن عائلات</option>
							<option value="residential_singles">سكن أفراد</option>
							<option value="commercial">تجاري</option>
							<option value="mixed">مختلط / أخرى</option>
						</select>
				</div>
			</div>
		</div><!-- /digitalSuck -->


		<div v-if="inputs.step_1.F4_suckType == 'bank' && inputs.step_4.gotit == 'no'">

			<div class="explain">بما أن العقار من خلال البنك ، وركز معانا 😊<br>
			البنك اعطاك حاجة اسمها (وثيقة التملك)
			شكلها زي الصك ، نحتاج منها معلومتين
			<div class="my-3 ms-2">
				1- الرقم<br>
				2- رقم السجل التجاري
			</div>

				الرقم مكون من 12 خانة تلاقيه فوووق على اليسار أما رقم السجل التجاري بتلاقيه تحت في السطر قبل الاخير بعد جملة (وقد انتقلت ملكيتها لـ ....)
				
				<ul class="btns my-3 text-center">
					<button	@click="inputs.step_4.explain == 'yes'" class="btn btn-light me-30">شرح اضافي</button>
					<button	@click="inputs.step_4.gotit == 'yes'" class="btn btn-success ms-30">واضح</button>
				</ul>
			</div>
			
			<div class="showBankSuck mb-3">

				<div class="row">
					<input type="text" dir="ltr" v-model="inputs.step_4.F4_bankCR" inputmode="numeric" class="input100" maxlength="10" placeholder="رقم السجل التجاري للبنك (10 أرقام)"/>
				</div>

				<div class="row">
					<input type="text" dir="ltr" v-model="inputs.step_4.F1_suckNumber" inputmode="numeric" class="input100" maxlength="12" placeholder="رقم الصك الإلكتروني (12 رقم)"/>
				</div>

				<div class="d-flex justify-content-between mb-3">
					<input type="text" v-model="inputs.step_4.F2_suckDate" class="RollDate7 input50 me-15" readonly placeholder="تاريخ الصك"/>
					<select class="input50 ms-15" v-model="inputs.step_4.F6_propertyType">
						<option value="">حدد نوع العقار</option>
						<option value="building">عمارة</option>
						<option value="villa">فيلا</option>
						<option value="plaza">بلازا</option>
						<option value="shopping_mall">مول</option>
						<option value="tower">برج</option>
						<option value="land">أرض</option>
						<option value="other">أخرى</option>
					</select>
				</div>	
				
				<div class="d-flex justify-content-between">			
					<select class="input50 me-15" v-model="inputs.step_4.F7_propertyUse">
						<option value="">استخدام المبنى</option>
						<option value="residential_families">سكن عائلات</option>
						<option value="residential_singles">سكن أفراد</option>
						<option value="commercial">تجاري</option>
						<option value="mixed">مختلط / أخرى</option>
					</select>
					<input type="text" dir="ltr" inputmode="numeric" class="input50 ms-15" maxlength="2" placeholder="عدد أدوار المبنى"/>

				</div>
			</div>
		</div>


		<div class="text-center" v-if="inputs.step_1.F4_suckType == 'old'">
			الله يسعدك حاول تكون صورة الصك واضحة ومقروءة عشان ننجز معاملتك

			<div class="d-flex justify-content-between mt-3">
				<div class="col-md-12 mb-3">
					<div class="UploadFile pointer btn btn-light w-100" role="button" style="border-radius:10px">ارفاق هنا صورة الصك القديم</div>
					<input type='file' name='SuckDoc' class="d-none SuckDoc" id="SuckDoc">
				</div>				
			</div>	

			<div class="row">
				<select class="input100" v-model="inputs.step_4.F6_propertyType">
					<option value="">حدد نوع العقار</option>
					<option value="building">عمارة</option>
					<option value="villa">فيلا</option>
					<option value="plaza">بلازا</option>
					<option value="shopping_mall">مول</option>
					<option value="tower">برج</option>
					<option value="land">أرض</option>
					<option value="other">أخرى</option>
				</select>
			</div>	
			
			<div class="d-flex justify-content-between">			
				<select class="input50" v-model="inputs.step_4.F7_propertyUse">
					<option value="">استخدام المبنى</option>
					<option value="residential_families">سكن عائلات</option>
					<option value="residential_singles">سكن أفراد</option>
					<option value="commercial">تجاري</option>
					<option value="mixed">مختلط / أخرى</option>
				</select>
				<input type="text" dir="ltr" inputmode="numeric" class="input50" maxlength="2" placeholder="عدد أدوار المبنى"/>

			</div>

		</div><!-- /oldSuck -->


		<div class="d-none form-group WakeelWaratha Representative" data-type="ReprID">
			<input class="checkuser mt-0" dir="ltr" type="text" inputmode="numeric" maxlength="10" pattern="[1-2]{1}[0-9]{9}$" placeholder="رقم هوية الوكيل الشرعي"/>
			<div class="d-none inputs">
				<div class="d-flex justify-content-between">
					<div class="col-md-12 mb-3 mt-3">
						<input type="text" placeholder="الاسم الثلاثي للوكيل الشرعي"/>
					</div>
				</div>
				<div class="col-md-12 mb-3 wakeelIban">
					<label class="error iban_error">رقم الآيبان غير صحيح</label>
				</div>
				<div class="col-md-12 mb-3">
					<input dir="ltr" type="text" inputmode="numeric" name="wakala" id="wakala" placeholder="رقم الوكالة"/>
				</div>
				<div class="d-flex justify-content-between">
					<div class="col-md-6 col-sm-6 col-6">
						<input class="checkmobile" dir="ltr" type="text" inputmode="numeric" maxlength="10" pattern="05[0-9]{8}$" placeholder="رقم جوال الوكيل"/>
					</div>
					<div class="col-md-6 col-sm-6 col-6">
						<input type="text" name="repr_birthday" id="repr_birthday" class="RollDate8" readonly  placeholder="تاريخ ميلاده"/>
					</div>				
				</div>
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