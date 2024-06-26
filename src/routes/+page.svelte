<svelte:head>
    
    <title>Calculator</title>

</svelte:head>

<script lang="ts">
    import { onMount } from "svelte";


    function addToquation(value:string){
        equation += value;
   }

   function backspace() {
           switch (equation.substring(equation.length - 3, equation.length)) {
               case " + ":
               case " - ":
               case " * ":
               case " / ":
                   equation = equation.substring(0, equation.length - 3);
                   break;
               default:
                   equation = equation.substring(0, equation.length - 1);
           }
       }

  

   function deleteAll(){
    equation = "";
   }


   
   function solve() {
        try {
            let answer = eval(equation);
            if (answer == undefined)
             throw SyntaxError;
            equation = answer;
             } catch (error) {
            let output = document.getElementById('output');
            output?.classList.add('bg-red-500');
            output?.classList.add('shadow-red-500');
            setTimeout(() => {
                output?.classList.remove('bg-red-500');
                output?.classList.remove('shadow-red-500');
            }, 500);
        }
    }

    let equation: string = ""; 
    
    function onKeyDown(e: KeyboardEvent) {
        let button = document.getElementById(e.key);
        button?.click();
        button?.focus();
        setTimeout(() => {
            document.activeElement?.blur();
        }, 100);
    }

    onMount(() => {
        let allButtons = document.getElementsByTagName('button');
        for (let i = 0; i < allButtons.length; i++) {
            allButtons[i].addEventListener('click', () => {
                new Audio('/click.wav').play();
            });
        }
    });
</script>
    <svelte:window on:keydown|preventDefault={onKeyDown} />

<div class="bg-[#e6e7eb]  h-[100dvh] flex justify-center items-center  ">


    <div  class="bg-white   rounded-3xl grid grid-cols-4 gap-1 p-6 shadow-2xl shadow-[#6f758d] max-w-[20rem]">
        <div id="output" class="bg-blue-500  text-white text-2xl rounded-xl col-span-4 min-h-16 items-center flex px-4 mb-2  max-w-[20rem] shadow-2xl shadow-[#3b82f6] break-all transition-all">
       {equation}
        </div>
    
    <button id="%" on:click={() => addToquation(' / 100')} class="bg-[#f3f6fc]"> % </button>
    <!-- backspace -->
    <button id="Backspace" on:click={backspace} class="bg-[#f3f6fc] flex items-center justify-center"> <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24"><path fill="currentColor" d="M18.75 4a3.25 3.25 0 0 1 3.245 3.066L22 7.25v9.5a3.25 3.25 0 0 1-3.066 3.245L18.75 20h-8.501a3.25 3.25 0 0 1-2.085-.756l-.155-.139l-4.995-4.75a3.25 3.25 0 0 1-.116-4.594l.116-.116l4.995-4.75a3.25 3.25 0 0 1 2.032-.888L10.25 4zm-7.304 4.397a.75.75 0 0 0-1.049 1.05l.073.083L12.94 12l-2.47 2.47l-.073.084a.75.75 0 0 0 1.05 1.049l.083-.073L14 13.061l2.47 2.47l.084.072a.75.75 0 0 0 1.049-1.05l-.073-.083L15.061 12l2.47-2.47l.072-.084a.75.75 0 0 0-1.05-1.049l-.083.073L14 10.939l-2.47-2.47z"/></svg></button>
    <button id="Delete" on:click={deleteAll} class="bg-[#f3f6fc] "> C </button>
    <button id="+" on:click={() => addToquation(' + ')} class="bg-[#63dc74] text-white shadow-md shadow-[#63dc74]"> <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24"><path fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 12h7m7 0h-7m0 0V5m0 7v7"/></svg>  </button>
    <button id="7" on:click={() => addToquation('7')}> 7 </button>
    <button id="8" on:click={() => addToquation('8')}> 8 </button>
    <button id="9" on:click={() => addToquation('9')}> 9 </button>
    <!--minus-->
    <button id="-" on:click={() => addToquation(' - ')} class="bg-[#fd3f59] text-white shadow-md shadow-[red]"> <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24"><path fill="currentColor" d="M19 11H5a1 1 0 0 0 0 2h14a1 1 0 0 0 0-2"/></svg> </button>
    <button id="4" on:click={() => addToquation('4')}> 4 </button>
    <button id="5" on:click={() => addToquation('5')}> 5 </button>
    <button id="6" on:click={() => addToquation('6')}> 6 </button>
    <!--قسمه-->
    <button id="/" on:click={() => addToquation(' / ')} class="bg-[#2285fd] text-white shadow-md shadow-[#2285fd]"> <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24"><g fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"><circle cx="12" cy="6" r="1" fill="currentColor"/><circle cx="12" cy="18" r="1" fill="currentColor"/><path d="M5 12h14"/></g></svg></button>
    <button id="1" on:click={() => addToquation('1')}> 1 </button>
    <button id="2" on:click={() => addToquation('2')}> 2 </button>
    <button id="3" on:click={() => addToquation('3')}> 3 </button>
    <!--multiply-->
    <button id="x" on:click={  () => addToquation(' * ')} class="bg-[#f9c80e] text-white shadow-md shadow-[#f9c80e]"> <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24"><path fill="currentColor" d="m13.41 12l6.3-6.29a1 1 0 1 0-1.42-1.42L12 10.59l-6.29-6.3a1 1 0 0 0-1.42 1.42l6.3 6.29l-6.3 6.29a1 1 0 0 0 0 1.42a1 1 0 0 0 1.42 0l6.29-6.3l6.29 6.3a1 1 0 0 0 1.42 0a1 1 0 0 0 0-1.42Z"/></svg> </button>
    <button id="." on:click={() => addToquation('.')}> . </button>
    <button id="0" on:click={() => addToquation('0')}> 0 </button>
    <button id="Enter" on:click={()=>solve()} class="bg-[#1f2b54] text-white shadow-md shadow-[#1f2b54] col-span-2  w-[8rem] "> = </button>
    <!--plus-->
    
</div>
</div>