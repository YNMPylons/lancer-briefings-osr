<template>
	<div id="factionsView" :class="{ animate: animateView }" :style="{ 'animation-delay': animationDelay }" class="content-container">
		<section id="factions" :class="{ animate: animate }" class="section-container">
			<div class="section-header clipped-medium-backward">
				<img src="/icons/squad.svg" />
				<h1>FACTIONS</h1>
			</div>
			<div class="section-content-container">
				<div class="events-list-container">
					<Event
						v-for="item in events"
						:key="item.title"
						:event="item"
						:animate="animate"
						@select-event="selectEvent(item)" />
				</div>
			</div>
		</section>
		<section id="overview" :class="{ animate: animate }" class="section-container">
			<div style="height: 52px; overflow: hidden">
				<div class="section-header clipped-medium-backward-overview">
					<img src="/icons/conversation.svg" />
					<h1>OVERVIEW</h1>
				</div>
				<div class="rhombus-back">&nbsp;</div>
			</div>
			<div class="section-content-container extra-margins">
				<div class="event" v-if="selectedEvent.title">
					<div class="name">
						<h1>{{ selectedEvent.location }} // {{ selectedEvent.time }}</h1>
						<h2>{{ selectedEvent.title }}</h2>
					</div>
					<vue-markdown-it :source="selectedEvent.content" class="markdown" />
				</div>
			</div>
		</section>
	</div>
</template>

<script>
import { VueMarkdownIt } from '@f3ve/vue-markdown-it';
import Faction from "@/components/Faction.vue";

export default {
	components: {
		VueMarkdownIt,
		Faction,
	},
	props: {
		animate: {
			type: Boolean,
			required: true,
		},
		events: {
			type: Array,
			required: true,
		},
	},
	data() {
		return {
			selectedFaction:{
				type: Object,
			}
		};
	},
	methods: {
		selectFaction(faction) {
			this.selectedFaction = faction;
		}
	}
};
</script>
