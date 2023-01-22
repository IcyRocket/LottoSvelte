<script>
	let start = 4
	let joker = false
	let trackr = 5
	let rewards = [{number: "2 196 000 kr", class: ""},{number: "1 464 000 kr", class: ""},{number: "1 010 000 kr", class: ""},{number: "722 000 kr", class: ""}, {number: "535 000 kr", class: ""},{number: "412 000 kr", class: "current"},]
	class Row{
		constructor(){
			this.classUbutton = "beforeclicked"
			this.classDbutton = "beforeclicked"
			this.ubuttoncontent = ""
			this.dbuttoncontent = ""
			this.arrowUp = ""
			this.arrowDown = ""
			this.classNumber = ""
			this.number = (Math.random()*9).toFixed(0)
			this.upperBetValue = (Math.random()*10).toFixed(0)
			this.downBetValue = (Math.random()*10).toFixed(0)
		}
		handleClick(index, element){
			console.log(index)
			if(index == start){
				rows[index].arrowUp = ""
				rows[index].arrowDown =  ""
				rows[index].classUbutton = "beforeclicked"
				rows[index].classDbutton = "beforeclicked"
				if(element.getAttribute('key') == "up"){
					if(rows[index].upperBetValue >= rows[index].number){
						if(rows[index].upperBetValue == 10){
							rows[index].classUbutton = "clickedbutton green"
							rows[index].arrowUp = "joker"
							joker = true
							joker = joker
							rewards[trackr].class = ""
							rewards[0].class ="current"
							trackr = 0
						}
						else{
							rows[index].classUbutton = "clickedbutton green"
							rows[index].ubuttoncontent = rows[index].upperBetValue
							if(index === 0){
								joker = true
							}
							if(trackr > 0){
								rewards[trackr].class = ""
								rewards[trackr-1].class = "current"
								trackr -= 1
							}
						}
						
					}
					else if(rows[index].upperBetValue < rows[index].number){
						if(rows[index].upperBetValue == 10){
							rows[index].classUbutton = "clickedbutton green"
							rows[index].arrowUp = "joker"
							joker = true
							joker = joker
							rewards[trackr].class = ""
							rewards[0].class ="current"
							trackr = 0
						}
						else{
							rows[index].classUbutton = "clickedbutton red"
							rows[index].ubuttoncontent = rows[index].upperBetValue
							if(index === 0){
								joker = true
							}
						}
					}
				}
				else if(element.getAttribute('key') == "down"){
					if(rows[index].downBetValue <= rows[index].number){
						if(rows[index].downBetValue == 10){
							rows[index].classDbutton = "clickedbutton green"
							rows[index].arrowUp = "joker"
							joker = true
							joker = joker
							rewards[trackr].class = ""
							rewards[0].class ="current"
							trackr = 0
						}
						else{
							rows[index].classDbutton = "clickedbutton green"
							rows[index].dbuttoncontent = rows[index].downBetValue
							if(trackr > 0){
								rewards[trackr].class = ""
								rewards[trackr-1].class = "current"
								trackr -= 1
							}
							if(index === 0){
								joker = true
							}
							
						}
					}
					else if(rows[index].downBetValue > rows[index].number){
						if(rows[index].downBetValue == 10){
							rows[index].classDbutton = "clickedbutton green"
							rows[index].arrowUp = "joker"
							joker = true
							joker = joker
							rewards[trackr].class = ""
							rewards[0].class ="current"
							trackr = 0
						}
						else{
							rows[index].classDbutton = "clickedbutton red"
							rows[index].dbuttoncontent = rows[index].downBetValue
							if(index === 0){
								joker = true
							}
						}
					}
				}
				if(joker == false){
					rows[index-1].arrowUp = "arrow up"
					rows[index-1].arrowDown = "arrow down"
					rows[index-1].classUbutton = "currentbutton"
					rows[index-1].classDbutton = "currentbutton"
					start > 0 ? start -= 1: start = 4
				}
				

			}
		
		}
	}
	function Reset(){
		window.location.reload()
	}
	let rows = [new Row(), new Row(), new Row(), new Row(), new Row()]

	rows[4].arrowUp = "arrow up"
	rows[4].arrowDown =  "arrow down"
	rows[4].classUbutton = "currentbutton"
	rows[4].classDbutton = "currentbutton"
</script>

<main>
	<div class="whole">
		{#if joker}
		<div class="title">
			<h1>Du vant {rewards[trackr].number}!</h1>
		</div>
		<div>
			
		</div>
		{/if}
		<div class="lottorow">
		{#each rows as row, index}	
			<div class="adjust">
				<!-- svelte-ignore a11y-click-events-have-key-events -->
				<div key="up" class={row.classUbutton} on:click={(event) =>{row.handleClick(index, event.currentTarget)}}>
					<div class={row.arrowUp}>{row.ubuttoncontent}</div>
				</div>
				<div class="number">
					<div>{row.number}</div>
				</div>
				<!-- svelte-ignore a11y-click-events-have-key-events -->
				<div key="down" class={row.classDbutton} on:click={(event) =>{row.handleClick(index, event.currentTarget)}}>
					<div class={row.arrowDown}> {row.dbuttoncontent}</div>
				</div>
			</div>
		{/each}
		{#if joker}
		<div>
			<button on:click={Reset} class="reset">Spill igjen</button>
		</div>
		{/if}
		</div>
		<div>
			{#each rewards as object}
			<p class={object.class}>{object.number}</p>
			{/each}
		</div>
	</div>
</main>

