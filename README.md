[back to assessments](https://github.com/dr-matt-smith/FEDev---assessment-samples-and-walkthroughs?tab=readme-ov-file) <<<

[Question 1](https://github.com/dr-matt-smith/FEDev---sample-lab-test-question-1)
| [Question 2](https://github.com/dr-matt-smith/FEDev---sample-lab-test-question-2)
| [Question 3](https://github.com/dr-matt-smith/FEDev---sample-lab-test-question-3)
|
Question 4
| [Question 5](https://github.com/dr-matt-smith/FEDev---sample-lab-test-question-5)
| [Question 6](https://github.com/dr-matt-smith/FEDev---sample-lab-test-question-6)


# FEDEv - SAMPLE lab test question 4

The "brief" for the test is a PDF file in directory "brief"

NOTE:
**no use of AI is permitted in the lab test**

There are videos for each of the 6 questions:


The files in this repo are the solution I created to this sample test
- you may use any editor available on the university PCs
  - I used Celbridge, which you may install on the lab PCs if you wish

## Question 4 - video

- question 4
  - https://go.screenpal.com/watch/cOehrbnZFYO
  - 10mins 52secs


## Question 4a - page created objects and loop to display  `/food`

We need to create a directory `/routes/food`. And in this directory a Svelte page script `/routes/food/+page.svelte`.

First, let's define a JSON array for the 3 foods:

```html
<script>
  const foods = [
    {   "name": "lemon juice",
      "ph": 2
    },
    {   "name": "lettuce",
      "ph": 7
    },
    {   "name": "apples",
      "ph": 4
    }
  ];
</script>
```

Next loop through to display the 2 columns 

```html
<table>
  <tbody>
  
    {#each foods as food}
    <tr>
        <td>{food.name}</td>
        <td>{food.ph}</td>
    </tr>
    {/each}

  </tbody>
</table>
```

## Question 4b - add third column using function from question 2

We need to first import the function from the utility file:

```html
<script>
    import { isNeutral } from '$lib/util/useful_functions.js';

    const foods = [
        {   "name": "lemon juice",
            "ph": 2
        },
            ...
    ];
</script>
```

We can then add a Svelte IF-statement, to decide which message to display for each row:

```html
<table>
  <tbody>

  {#each foods as food}
  <tr>
    <td>{food.name}</td>
    <td>{food.ph}</td>
    <td>
      {#if isNeutral(food.ph)}
      Neutral
      {:else}
      Acidic or alkaline
      {/if}
    </td>
  </tr>
  {/each}

  </tbody>
</table>
```

Finally, let's add a little CSS to make the table look a bit nicer (you don't have to do this in the real test unless asked explicitly...):

```html
<style>
  table, td, tr  {
    border: 1px solid black;
  }

  td {
    padding: 1rem;
    width: 12rem;
    text-align: center;
  }
</style>
```

So the final full listing is as follows:

`/routes/food/+page.svelte`

```html
<script>
  import { isNeutral } from '$lib/util/useful_functions.js';

  const foods = [
    {   "name": "lemon juice",
      "ph": 2
    },
    {   "name": "lettuce",
      "ph": 7
    },
    {   "name": "apples",
      "ph": 4
    }
  ];
</script>

<table>
  <tbody>

  {#each foods as food}
  <tr>
    <td>{food.name}</td>
    <td>{food.ph}</td>
    <td>
      {#if isNeutral(food.ph)}
      Neutral
      {:else}
      Acidic or alkaline
      {/if}
    </td>
  </tr>
  {/each}

  </tbody>
</table>

<style>
  table, td, tr  {
    border: 1px solid black;
  }

  td {
    padding: 1rem;
    width: 12rem;
    text-align: center;
  }
</style>
```



## Question 4c - add route to global site navbar

We need to add a link to this page in the site navbar


```html
<a href="/">home</a>
|
<a href="/privacy">privacy</a>
|
<a href="/food">food</a>
...
```

The full listing for our site layout page now looks as follows;

`/routes/+layout.svelte`

```html
<script>
  import favicon from '$lib/assets/favicon.svg';

  let { children } = $props();
</script>

<svelte:head>
  <link rel="icon" href={favicon} />
</svelte:head>

<nav>
  <a href="/">home</a>
  |
  <a href="/privacy">privacy</a>
  |
  <a href="/food">food</a>
  |
  <a href="/evenform">form to input number and test its even'ness</a>
</nav>
<hr>

{@render children()}
```