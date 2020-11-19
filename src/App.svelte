<script>
	import {randexp} from 'randexp'


	let big = true
	let lil = true
	let nums = true
	let symbols = true
	let count = 8
	let rando_string = ""
	let pass_span;
	function create(){
		rando_string = ""
		if(big){
			rando_string += randexp(`^[A-Z]{${count}}$`)
		}
		if(lil){
			rando_string +=  randexp(`^[a-z]{${count}}$`)
		}
		if(nums){
			rando_string +=  randexp(`^[0-9]{${count}}$`)
		}
		if(symbols){
			rando_string +=  randexp(`^[?=.*-+_!@#$%^&*., ?]{${count}}$`)
		}

		if(!big && !lil && !nums && !symbols){
			rando_string +=  randexp(`^[a-z]{${count}}$`)
		}
		rando_string = generatePassword(rando_string)
		
	}

	function generatePassword(pass){
		let shuffled = pass.split('').sort(function(){return 0.5-Math.random()}).join('');

		let password = shuffled.substring(0, count)
		return password
	}
	function copy(){
		let textarea = document.createElement("textarea")
		textarea.value = rando_string
		document.body.appendChild(textarea)
		textarea.select()
		document.execCommand('copy')
		if(rando_string.length > 2){
			alert('رمز ساخته شده کپی شد')
		}else{
			alert('رمز ساخته شده کپی شد')
		}
		document.body.removeChild(textarea)
	}
	
</script>

<svelte:head>
	<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
	<script src="https://github.com/fent/randexp.js/releases/download/v0.4.3/randexp.min.js"></script>
</svelte:head>
<main>
	<div class="container">
		<h2>تولید رمز عبور</h2>
		<div id="password-show">
			<i class="fa fa-clipboard" on:click="{copy}"></i>
			<span bind:this={pass_span}>{rando_string}</span>
		</div>
		<div id="password-length">
			<input type="number" min="8" max="127" name="length" id="length" bind:value="{count}">
			<span>طول رمز</span>
		</div>
		<div id="password-length">
			<input type="checkbox" name="big-chars" id="bigchars" bind:checked={big}>
			<span>شامل حروف بزرگ باشد</span>
		</div>
		<div id="password-length">
			<input type="checkbox" name="lil-chars" id="bigchars" bind:checked={lil}>
			<span>شامل حروف کوچک باشد</span>
		</div>
		<div id="password-length">
			<input type="checkbox" name="nums" id="bigchars" bind:checked={nums}>
			<span>شامل اعداد  باشد</span>
		</div>
		<div id="password-length">
			<input type="checkbox" name="symbols" id="bigchars" bind:checked={symbols}>
			<span>شامل علائم باشد</span>
		</div>
		<button on:click="{create}">بساز</button>
	</div>
</main>

<style>
	.container{
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		margin: 0;
		padding: 0;
		width: 400px;
		min-width: 400px;
		max-width: 400px;
		border-radius: 10px;
		background-color: navy;
		color: white;
	}
	button{
		width: 75%;
		margin: 20px auto;
		padding: 5px 5px;
		font-weight: bold;
		font-size: 20px;
		background-color: #6080d0;
		outline: none;
		border: none;
		color: white;
		cursor: pointer;
		border-radius: 6px;
	}
	#password-length{
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		width: 75%;
		/* min-width: 300px; */
		margin-top: 20px;
		font-weight: bold;
	}
	#password-show{
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		background-color: #000;
		width: 300px;
		min-width: 300px;
		border-radius: 6px;
	}
	#password-show i{
		margin: 10px;
		padding: 10px;
		background-color: #6080d0;
		border-radius: 6px;
		color: white;
		cursor: pointer;
	}
	#password-show span{
		padding-right: 15px;
		color: white;
		max-height: 50px;

		overflow: hidden;
		text-overflow: ellipsis;

	}
	
</style>