<template>
	<div class="container">
	    <div class="row">
	        <div class="col-md-7 col-md-offset-2">
	            <form class="form-horizontal">
	                <div class="alert"
	                     v-for="error in errors">{{error}}
	                </div>
	                <h1>Rangschik de volgende mogelijke voordelen van de AD Nieuwsapp van meest naar minst belangrijk</h1>
	                <div class="form-group">

	                    <div class="col-sm-12">
	                        <input type="text"
	                               class="form-control"
	                               v-model="newItem"
	                               placeholder="Voeg zelf een voordeel toe"
	                               id="todo">
	                    </div>
	                </div>
	                <div class="form-group">
	                    <div class="col-sm-6">
	                        <button v-on:click.prevent="addItem()"
	                                class="btn btn-primary btn-block btn-color">Voordeel toevoegen
	                        </button>
	                    </div>
	                </div>
	            </form>

	            <ol class="list-group">
	                <draggable class="dragArea" :options="{ghostClass: 'ghost'}">
		                <li class="voordeel" v-for="definedItem in definedItems">
							{{definedItem}}
		                </li>

		                <li class="voordeel list-group-item--bold" v-for="item in itemList">
		                    <button type="button" class="close" v-on:click.prevent="deleteItem(item)">
		                		<span>x</span>
		                    </button>
		                    {{item}}
		                </li>
	            	</draggable>
	            </ol>
	        </div>
	    </div>
	</div>
</template>

<script>
	import draggable from 'vuedraggable'

	export default {
		components: {
			draggable
		},
	    data () {
	        return {
	            definedItems: [
	            	"De kwaliteit van artikelen en video's",
	            	"De bundeling van 4 in 1 apps",
	            	"De toevoeging van een uitgebreid video-aanbod",
	            	"De gebruiksvriendelijkheid waarmee je je door de app beweegt",
	            	"Alles wat speelt in de regio's die je interesseren",
	            	"Al het belangrijkste nationale en internationale nieuws",
	            	"Een gepersonaliseerde nieuwsstroom uit verschillende kranten"
	            ],
	            itemList: [],
	            newItem: '',
	            errors: []
	        }
	    },
	    methods: {
	        addItem: function () {
	            var tempItem = this.newItem;

	            // Empty the errors
	            this.errors = [];

	            // Check if value is filled in
	            if (tempItem) {
	                this.itemList.unshift(tempItem);
	            } else {
	                this.errors.push('Je moet nog een item ingeven');
	            }

	            // empty input
	            this.newItem = '';
	        },
	        deleteItem: function (item) {
	            this.itemList.pop(item);
	        }
	    }
	}
</script>

<style>
	.alert {
		display: block;
		background: red;
		color: white;
	}

	h1 {
		padding-bottom: 15px;
		font-size: 24px;
		line-height: 1.3;
	}

	.ghost {
		background: #e6fff2;
	}

	.btn-color {
		background-color: #DB011B;
		border-color: #DB011B;
	}

	.list-group-item {
		list-style-type: decimal!important;
	}

	.list-group-item--bold {
		font-weight: bold;
	}

	.voordeel {
		border: 1px solid #CCC;
		border-bottom: 0;
		list-style-position: inside;
		padding: 7px 10px;
		font-size: 18px;
	}
	.voordeel:last-child {
		border-bottom: 1px solid #CCC;;
	}
</style>
