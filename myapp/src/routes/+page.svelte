<script>
	let total = 0;
	let console = "";
	let state = null;
	function resolveState(){
		switch(state){
			case "add":
				total += parseFloat(console);
				console = "0";
				break;
			case "substract":
				total -= parseFloat(console);
				console = "0";
				break;
			case "multiply":
				total *= parseFloat(console);
				console = "0";
				break;
			case "divide":
				total /= parseFloat(console);
				console = "0";
				break;
			default:
				total = parseFloat(console);
				console = "0";
				break;
		}
	}
	function setOperation(operation){
		resolveState();
		state = operation;
	}
	function setValue(value){
		if(console.toString() == "0" || state == "equal"){
			console = "";
		}
		if(state == "equal"){
			state = null;
		}
		if(value == "C"){
			total = 0;
			state = null;
			console = "";
			return;
		}
		console = console + value;
	}
	function equal(){
		resolveState();
		console = total;
		state = "equal";
	}
</script>
<style>
	.calculator {
		position:absolute;
		top:50%;
		left:50%;
		transform:translate(-50%,-50%);
		width:300px;
		border:1px solid #eee;
		box-shadow:2px 2px 2px #eee;
		padding:10px;
	}
	.calculator input {
		width:100%;
		padding:10px;
		outline:none;
		text-align:right;
		font-size:20px;
	}
	.calculator .buttons {
		display:flex;
		flex-wrap:wrap;
	}
	.calculator .buttons .operations {
		display:flex;
		justify-content:space-between;
		width:100%;
	}
	.calculator .buttons .operations button {
		width:22%;
	}
	.calculator .buttons .numbers {
		width:100%;
	}
	.calculator .buttons .numbers {
		display:flex;
		justify-content:space-between;
	}
	.calculator .buttons .numbers div button {
		width:100%;
	}
	.calculator .equal {
		flex:1;
	}
	.calculator .equal button {
		margin-left:2.5%;
		width:95%;
		height:95%;
		background:#00acee;
		color:#eee;
	}
	.calculator button {
		outline:black;
	}
</style>
<div class="calculator">
    <input type="text" bind:value={console} readonly="true"/>
    <div class="buttons">
        <div class="operations">
            <button on:click={()=>{setOperation('add');}}>+</button>
            <button on:click={()=>{setOperation('subtract');}}>-</button>
            <button on:click={()=>{setOperation('multiply');}}>
            &times;</button>
            <button on:click={()=>{setOperation('divide');}}>&divide;</button>
        </div>
        <div class="numbers">
            <button on:click={()=>{setValue(9);}}>9</button>
            <button on:click={()=>{setValue(8);}}>8</button>
            <button on:click={()=>{setValue(7);}}>7</button>
        </div>
        <div class="numbers">
            <button on:click={()=>{setValue(6);}}>6</button>
            <button on:click={()=>{setValue(5);}}>5</button>
            <button on:click={()=>{setValue(4);}}>4</button>
        </div>
        <div class="numbers">
            <button on:click={()=>{setValue(3);}}>3</button>
            <button on:click={()=>{setValue(2);}}>2</button>
            <button on:click={()=>{setValue(1);}}>1</button>
        </div>
        <div class="numbers">
            <button on:click={()=>{setValue(0);}}>0</button>
            <button on:click={()=>{setValue('.');}}>.</button>
            <button on:click={()=>{setValue(C);}}>C</button>
        </div>
        <div class="equal">
            <button on:click={equal}>=</button>
        </div>
    </div>

</div>