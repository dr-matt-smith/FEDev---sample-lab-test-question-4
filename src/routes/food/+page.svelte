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