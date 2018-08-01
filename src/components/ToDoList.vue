<template>
	<main role="main">		
		<div class="container" aria-labelledby="todos-label">
			<h1 id="todos-label" tabindex="-1"><span>ma </span>{{ title }}</h1>
			<div id="decor">&nbsp;</div>
			<div class="wrapper">
				<form @submit.prevent="addNewItem">
					<!-- The label element is for accessibility purpose -->						
					<label for="add" class="vh">Saisir une nouvelle tâche</label>				            
					<input 
						type="text" 
						id="add" 
						placeholder="Ajouter une tâche"						
						v-model.trim="newItem" 						
						@keyup.esc="clearInputField"
						@focus="clearInputField"
						aria-invalid="true"
						aria-label="Ajouter une tâche"
					/>
					<button type="submit" :disabled="validated" :class="{active: isActive, desactive: hasError}">ajouter</button>
					<p class="warning" v-show="inError"> " {{ newItem }} " existe déjà !</p>					
				</form>	
				<article class="info" v-if="!todos.length">
					<h2>bravo !</h2>
					<p>
						Vous n'avez plus rien à faire<br />
						...Mais en êtes-vous certain ?
					</p>
				</article>		
				<ul>
					<li v-for="todo in unCompleted" :key="todo.item" @click="switchStatus(todo)">
						<input 
							type="checkbox" 														
							v-model="todo.done"
							:id="todo.item"													
						/>
						<label :for="todo.item">
							<span>{{ todo.item }}</span>						
						</label>
						<button @click.stop="onRemove(todo)" class="delete-btn" :aria-label="`delete ${todo.item}`">&times;</button>
					</li>					
				</ul>
				<ul>
					<li v-for="todo in completed" :key="todo.item" @click="switchStatus(todo)">
						<input 
							type="checkbox" 							 
							v-model="todo.done"	
							:id="todo.item"						
						/>
						<label :for="todo.item">
							<span class="text">{{ todo.item }}</span>
						</label>
						<button @click.stop="onRemove(todo)" class="delete-btn" :aria-label="`delete ${todo.item}`">&times;</button>
					</li>					
				</ul>				
			</div>
		</div>		
	</main>   
</template>

<script>
export default {	
  name: "ToDoList",  
  data() {
	return {
		title: 'to do list',

		todos: [			
			{
				item: "Assurer la responsive",
				done: true
			},
			{
				item: "Rendre le monde accessible",
				done: false
			},
			{
				item: "Dominer le monde à l'aide du JS",
				done: false
			},
			{
				item: "Rejoindre OUI.sncf",
				done: true
			}
		],

		newItem: '',

		inError: false,

		isActive: true,
		hasError: false,
		
		};
	},
	
	methods: {
		checkExistedItem(str, event){
			const existItems = this.todos.map((task) => task.item);				
			if(existItems.includes(str)) {				
				return true;
			}else{
				return false;
			}				
		},

		addNewItem(todo, item){
			const text = this.newItem.charAt(0).toUpperCase() + this.newItem.slice(1);			
			if(this.checkExistedItem(text)) {
				this.inError = true;
				this.hasError = true;
							 
			}else{				
				this.todos.push({
					item: text,
					done: false
				});
				this.newItem = '';		
				this.inError = false;
				this.hasError = false;
			}				
		},

		onRemove(todo) {	
			const currentItem = this.todos.indexOf(todo);
			this.todos.splice(currentItem, 1);	
			document.getElementById('todos-label').focus(); /* Accessibility */			
		},

		clearInputField(event) {
			event.target.value = '';
			this.newItem = '';
			this.inError = false;
			this.hasError = false;
		},

		switchStatus(todo) {
			todo.done = !todo.done; 
		},

		compare(a, b) {
			if(a.item < b.item){
				return -1;
			}
			if(a.item > b.item){
				return 1;				
			}
			return 0;
		}
	},

	computed: {
		unCompleted(){
			const unCompletedItem =  this.todos.filter((todo) => !todo.done);
			return unCompletedItem.sort(this.compare);
		},

		completed(){
			const completedItem = this.todos.filter((todo) => todo.done);
			return completedItem.sort(this.compare);
		},

		validated() {
			return this.newItem === '';
		}
	}
};
</script>

<style lang="scss" scoped>

main{
	position: relative;
	width: 333px;
	height: auto;
	margin: 43px 0 0 40px;
	grid-column: 5/9; 

  	.container{    
		position: relative;
		z-index: 10;

		padding-bottom: 30px;
		border-radius: 10px;			
	}

	.wrapper{
		position: relative;
		top: -20px;
		z-index: 10;

		width: 332px;
		min-height: 230px;
		padding-bottom: 30px;

		border-radius: 0 0 10px 10px;
		border: 1px solid #e0ddd9;
		border-top: 0;		
	}	
} 

#todos-label{
	font-family: 'Baloo', sans-serif;
	font-size: 2.25rem;
	color: #ffffff;
	text-transform: capitalize;

	padding: 35px 75px 80px 30px;	

	background: #3e4647;
	background: linear-gradient(48deg, rgba(116,198,213,1) 0%, rgba(65,165,182,1) 100%);	
	
	border-radius: 10px 10px 0 0;
	border: 1px solid #e0ddd9;

	span{
		font-family: 'Roboto', sans-serif;
		font-size: 1.75rem;		
	}
}

#decor{
	position: absolute;
	top: 100px;
	left: -5px;
	z-index: 0;

	width: 105%;
	height: 100px;
		
	background-color: #ffffff;
	border-radius: 220px / 50px;
	transform:rotate(-8deg); 
}

form{
    margin: -30px 0 20px 0;
    position: relative;
    z-index: 2;
    padding: 50px 0 0 30px;

	button[type="submit"]{
		display: inline-block;

		font-family: 'Baloo', sans-serif;
		text-transform: capitalize;	
	
		background-color: #ffffff;	
		border-radius: 20px;		
		padding: 3px 10px;
		cursor: default;
		
	
		&.active{
			color: #24b187;
			border: 1px solid #24b187;
			cursor: pointer;
		}

		&.desactive,
		&[disabled]{
			color: #ea5330;
			border-color: #ea5330;
			cursor: default;
		}
    }

    input[type="text"]{
        width: 200px;
        margin-right: 10px;
		padding: 5px;

		color: #66625b;
		background-color: #ffffff;
		
        border: 0;
        border-bottom: 1px solid #e0ddd9;        
    }

	input:focus::-webkit-input-placeholder { 
		color: transparent; 
	}

	input:focus:-moz-placeholder { 
		color: transparent; 
	}

	.warning{
		font-size: 0.8rem;		
		font-weight: 500;
		color: #ea5330;
		margin-top: 5px;
	}
}

.delete-btn{
	display: none;
}

[tabindex="-1"]{
	outline: none;
}

.info{
	text-align: center;
	color: #3fa4b6;

	h2{
		text-transform: uppercase;
		font-weight: 700;
		margin-bottom: 5px;
	}

	p{
		font-size: 0.9rem;
		font-weight: 400;		
	}
}

/* Class makes sure the element(s) in question are not visible,
** but are still detected and announced in screen readers. ***/

.vh {
    position: absolute !important;
    clip: rect(1px, 1px, 1px, 1px);
    padding:0 !important;
    border:0 !important;
    height: 1px !important;
    width: 1px !important;
    overflow: hidden;
}

/********* Customize checkbox ***********
****************************************/
/* Hide default checkbox */
[type="checkbox"]:checked,
[type="checkbox"]:not(:checked){
	position: absolute;
	left: -9999px;
}

/* Style <label> */
[type="checkbox"]:checked + label,
[type="checkbox"]:not(:checked) + label{
	position: relative;
	padding-left: 25px;
	cursor: pointer;
}

/* :before for styling checkbox */
[type="checkbox"]:not(:checked) + label:before,
[type="checkbox"]:checked + label:before {
	content: '';
	position: absolute;
	left:0; 
	top: 2px;

	width: 14px; 
	height: 14px;

	border-radius: 3px; 
	border: 1px solid #999082;
	background: #ffffff;
}

[type="checkbox"]{
    &:checked + label .text {
      text-decoration: line-through;
	  color: #66625b;
	}
}

/* Styling checked mark */
[type="checkbox"]:not(:checked) + label:after,
[type="checkbox"]:checked + label:after {
	content: '\2713';
	position: absolute;
	top: 2px; 
	left: 0;

	width: 12px;
	height: 12px;
	padding: 2px 0 0 2px;

	font-size: 0.8rem;
	font-weight: 900;
	color: #ffffff;

	border-radius: 3px;
	border: 1px solid #e0ddd9;
	background: #e0ddd9;
	
	transition: all .5s;
}

/* not checked */
[type="checkbox"]:not(:checked) + label:after {
  	opacity: 0;
}

ul{
	padding-left: 30px;

	li{
		position: relative;
		margin-bottom: 10px;

		span{
			font-size: 0.875rem;
		}

		button{
			position: absolute;
			top: -12px;
			right: 20px;

			font-family: 'Roboto', sans-serif;
			font-size: 1.8rem;
			font-weight: 300;
			color: #999082;

			border: 0;			
			background-color: transparent;				
			cursor: pointer;
		}

		&:hover .delete-btn{
			display: block;
		}
	}
}    


/* Media Queries */

@media (max-width : 760px){
    main{
        grid-column: 3/7;
        grid-row: 2;
		margin: 40px auto 0 auto;
    }
}

@media (max-width : 560px){
    main{
        grid-column: 2/8;
		margin: 40px auto 0 auto;
    }
}

@media (max-width : 400px){
    main{
        grid-column: 1/9;
		margin: 40px auto 0 auto;
    }
}
</style>
