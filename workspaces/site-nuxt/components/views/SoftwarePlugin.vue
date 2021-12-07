<script>
	/** import used components */
	import BaseHeading from '@/components/BaseHeading';
	import BaseRichText from '@/components/BaseRichText';
	import BaseCardGraphic from '@/components/BaseCardGraphic';
	import BaseLayoutColumns from '@/components/BaseLayoutColumns';
	import BaseLayoutGrid from '@/components/BaseLayoutGrid';
	import SoftwarePluginDropdown from '@/components/SoftwarePluginDropdown';
	const shipStationLogo = require('@/assets/images/shipstation-logo.svg');
	export default {
		name: 'SoftwarePlugin',
		components: {
			BaseHeading,
			BaseRichText,
			BaseCardGraphic,
			BaseLayoutColumns,
			BaseLayoutGrid,
			SoftwarePluginDropdown,
		},
		props: {
			/** title of software plugin */
			pluginTitle: {
				type: String,
				required: true,
			},
			/** short description of software plugin */
			pluginDescription: {
				type: String,
				required: true,
			},
			/** price of software plugin */
			pluginPrice: {
				type: String,
				required: true,
			},
			/** version of software plugin */
			pluginVersion: {
				type: String,
				required: true,
			},
			/** date of software plugin last update in DD/MM/YYYY */
			pluginLastUpdate: {
				type: Date,
				required: true,
			},
			/** software plugin about information */
			pluginAbout: {
				type: Array,
				required: true,
			},
			/** selected software plugin compatibility */
			pluginCompatibility: {
				type: Object,
				required: true,
			},
			/** software plugin compatibilities */
			pluginCompatibilities: {
				type: Array,
				required: true,
			},
		},
		computed: {
			lastUpdated() {
				/** returns formatted date */
				const formattedDate = this.formatLastUpdatedDate(this.pluginLastUpdate);
				return formattedDate;
			},
		},
		data() {
			return {
				active: false,
				logo: shipStationLogo,
			};
		},
		methods: {
			/** accepts date in Date format
			 * returns date in DD/MM/YYYY format
			 */
			formatLastUpdatedDate(date) {
				const newDate = new Date(date);
				var dd = String(newDate.getDate());
				var mm = String(newDate.getMonth() + 1);
				var yyyy = newDate.getFullYear();
				return mm + '/' + dd + '/' + yyyy;
			},
		},
	};
</script>

<template>
	<main>
		<section class="bg-intro py-16 flex flex-col space-y-28">
			<div class="max-w-sm xl:max-w-xl mx-auto">
				<BaseLayoutColumns layout="thirds" align="left" valign="center" gap="none" element="div">
					<div class="space-y-10">
						<div class="h-full">
							<BaseHeading class="mb-4 filter drop-shadow-custom" :heading-level="3" :theme="'h3'">
								<span class="text-4xl xl:text-[56px]">{{ pluginTitle }}</span></BaseHeading
							>
							<div class="space-y-3">
								<BaseRichText
									:body="pluginDescription"
									:classes="'text-secondary text-lg xl:text-xl font-medium flex-wrap'"
								/>
							</div>
						</div>
						<div class="w-full xl:max-w-[624px]">
							<div class="flex flex-col space-y-3 xl:space-y-0 xl:flex-row justify-between">
								<div class="border-l-2 pl-5 border-secondary">
									<BaseHeading :heading-level="'2'" :theme="'h4'" class="mb-2">
										<span class="text-xl leading-6 font-medium">Version</span>
									</BaseHeading>
									<BaseRichText
										:body="pluginVersion"
										:classes="'text-primary text-lg xl:text-[32px] font-medium leading-[40px]'"
									/>
								</div>
								<div class="border-l-2 pl-5 border-secondary">
									<BaseHeading :heading-level="'2'" :theme="'h4'" class="mb-2">
										<span class="text-xl leading-6 font-medium">Last update</span>
									</BaseHeading>
									<BaseRichText
										:body="lastUpdated"
										:classes="'text-primary text-lg xl:text-[32px] font-medium leading-[40px]'"
									/>
								</div>
								<div class="border-l-2 pl-5 border-secondary">
									<BaseHeading :heading-level="'2'" :theme="'h4'" class="mb-2">
										<span class="text-xl leading-6 font-medium">Compatibility</span>
									</BaseHeading>
									<!-- Dropdown -->
									<SoftwarePluginDropdown
										:selected="pluginCompatibility"
										:options="pluginCompatibilities"
									/>
								</div>
							</div>
						</div>
					</div>
					<template v-slot:aside>
						<div class="min-w-full xl:min-w-[321px]">
							<BaseCardGraphic alignment="vertical">
								<div class="space-y-5">
									<p class="'text-primary text-6xl xl:text-7xl font-light leading-[108px]'">{{
										pluginPrice
									}}</p>
									<BaseButton
										:theme="'tertiery'"
										:rounded="false"
										:url="'https://fostercommerce.com'"
									>
										<span class="flex items-center text-lg xl:text-2xl text-highlight-secondary">
											Buy now
											<svg-icon
												:name="`icons/arrow-diagonal`"
												fill="currentColor"
												class="w-3 h-3 xl:w-[18px] xl:h-[18px] inline-flex"
											/>
										</span>
									</BaseButton>
								</div>
								<template v-slot:media>
									<BaseImage
										:src="logo"
										:imgClasses="'h-[260px] w-[260px] xl:h-[225.99px] xl:w-[225.99px] -mt-7'"
										alt="ShipStation Logo"
									/>
								</template>
							</BaseCardGraphic>
						</div>
					</template>
				</BaseLayoutColumns>
			</div>
			<div class="min-w-sm mx-auto md:items-center xl:min-w-3/4">
				<ul class="md:flex w-full justify-between">
					<li>
						<BaseLink
							:url="'https://fostercommerce.com/about'"
							:classes="'underline text-highlight-primary text-lg md:text-xl xl:text-2xl xl:leading-10 tracking-[0.02em]'"
							>About</BaseLink
						>
					</li>
					<li>
						<BaseLink
							:url="'https://fostercommerce.com/about'"
							:classes="'text-tertiery text-lg md:text-xl xl:text-2xl xl:leading-10 tracking-[0.02em]'"
							>Changelog</BaseLink
						>
					</li>
					<li>
						<BaseLink
							:url="'https://fostercommerce.com/about'"
							:classes="'flex items-center text-tertiery text-lg md:text-xl xl:text-2xl xl:leading-10 tracking-[0.02em]'"
						>
							Documentation
							<svg-icon
								:name="`icons/arrow-diagonal`"
								fill="currentColor"
								class="w-3 h-3 xl:w-[18px] xl:h-[18px] inline"
							/>
						</BaseLink>
					</li>
					<li>
						<BaseLink
							:url="'https://fostercommerce.com/about'"
							:classes="'flex items-center text-tertiery text-xl xl:text-2xl xl:leading-10 tracking-[0.02em]'"
						>
							Repository
							<svg-icon
								:name="`icons/arrow-diagonal`"
								fill="currentColor"
								class="w-3 h-3 xl:w-[18px] xl:h-[18px] inline"
							/>
						</BaseLink>
					</li>
				</ul>
			</div>
		</section>
		<section class="bg-body">
			<div class="py-10 max-w-sm mx-auto xl:max-w-3/4">
				<BaseHeading class="mb-4 xl:mb-6" :heading-level="'2'" :theme="'h2'">
					<span class="text-4xl xl:text-[56px] xl:leading-[78px]">About</span></BaseHeading
				>
				<div class="space-y-8">
					<BaseRichText
						v-for="about in pluginAbout"
						:key="about.id"
						:body="about"
						:classes="'text-tertiery leading-8 text-lg xl:text-[20px] font-medium text-lg xl:text-xl'"
					/>
				</div>
			</div>
		</section>
	</main>
</template>
