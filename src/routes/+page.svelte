<script lang="ts">
  const numbers = ["1", "5", "8", "7", "2", "3", "4", "6", "9", "0"];
  const operations = ["+", "+", "+", "+", "="];

  let operationSelecte = " ";
  let display = " ";
  let FirstNum = "";
  let secondNum = "";
  let isDisplayResult = false;

  const handleOperation = (operation: string) => {
    if (!FirstNum) return;
    if (operation === "=") {
      if (!secondNum) return;
      const FirstNumer = parseInt(FirstNum);
      const SecondNumer = parseInt(secondNum);

      let result = "";
      switch (operationSelecte) {
        case "/":
          result = (FirstNumer / SecondNumer).toFixed(2);
          break;
        case "*":
          result = (FirstNumer * SecondNumer).toFixed(2);
          break;
        case "-":
          result = (FirstNumer - SecondNumer).toFixed(2);
          break;
        case "+":
          result = (FirstNumer + SecondNumer).toFixed(2);
          break;
      }
      display = result;
      isDisplayResult = true;
    }
    operationSelecte = operation;
  };

  const handleClear = () => {
    FirstNum = "";
    secondNum = "";
    operationSelecte = "";
    display = "";
    isDisplayResult = false;
  };

  const handleNumberClick = (number: string) => {
    if (isDisplayResult) {
      handleClear();
    }
    if (display === "" && number === "0") return;

    if (number === "." && display.includes(".")) return;

    if (!operationSelecte) {
      if (display === "" && number === ".") {
        FirstNum = "0.";
        return (display = FirstNum);
      }
      FirstNum = `${FirstNum}${number}`;
      return (display = FirstNum);
    } else {
      if (display === "" && number === ".") {
        secondNum = "0.";
        return (display = secondNum);
      }
      secondNum = `${secondNum}${number}`;
      return (display = secondNum);
    }
  };
</script>

<main>
  <div class="calculator">
    <div class="results">{display}</div>
    <div class="digit">
      <div class="numbers">
        <button class="btn btn-xlg" on:click={handleClear}> C </button>
        {#each numbers as number (number)}
          <button
            class={`btn ${number === "0" ? "btn-lg" : null}`}
            on:click={() => handleNumberClick(number)}
          >
            {number}
          </button>
        {/each}
      </div>
      <div class="operations">
        {#each operations as operation (operation)}
          <button
            class={`btn ${
              operation === operationSelecte ? "btn-silver" : "btn-orange"
            }`}
            on:click={() => handleOperation(operation)}
          >
            {operation}
          </button>
        {/each}
      </div>
    </div>
  </div>
</main>

<style>

  main {
    width: 100vw;
    height: 100vh;
    display: flex;
    align-items: center;
    /* background-color: rgb(19, 233, 241); */
    justify-content: center;
  }
  .results {
    background-color: rgb(156, 213, 10);
    height: 60px;
    border-radius: 5px;
    font-size: 50px;
    display: flex;
    flex-direction: row-reverse;
    margin: 10px;
  }
  .calculator {
    background-color: #655bbb;
    width: 300px;
    padding: 20px;
    border-radius: 7px;
  }
  .numbers {
    display: flex;
    background-color: rgb(33, 21, 201);
    border-radius: 20px;

    flex-wrap: wrap;
    width: 200px;
    float: left;
    text-align: left;
  }
  .digits {
    display: flex;
  }
  .operations {
    display: flex;
    flex-direction: column; 
    border-radius: 20px;
    background-color: rgb(33, 21, 201);
    float: right;
    width: 30%;
    /* text-align: "right"; */
    justify-content: center;

  }
  .btn {
    width: 50px;
    height: 50px;
    border-radius: 100px;
    background-color: rgb(3, 3, 38);
    font-size: 20px;
    font-weight: bold;
    color: white;
    margin: 5px;
    border: rgb(241, 241, 4);
  }
  .btn-lg {
    width: 110px;
  }
  .btn-orange {
    background-color: orange;
  }
  .btn-xlg {
    width: 170px;
  }
  .btn-silver {
    background-color: silver;
  }
  .digits {
    display: flex;
  }
  .btn-black {
    background-color: black;
  }
</style>