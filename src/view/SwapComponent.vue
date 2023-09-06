<template>
    <div class="transactions">
        <div class="transactions-data">
            <table>
                <thead>
                    <tr>
                        <td>
                            <span class="table-heading">
                                id
                            </span>
                        </td>
                        <td>
                            <span class="table-heading">
                                sender
                            </span>
                        </td>
                        <td>
                            <span class="table-heading">
                                reciever
                            </span>
                        </td>
                        <td>
                            <span class="table-heading">
                                amount
                            </span>
                        </td>
                        <td>
                            <span class="table-heading">
                                timestamp
                            </span>
                        </td>
                        <td>
                            <span class="table-heading">
                                Token
                            </span>
                        </td>
                    </tr>
                </thead>
                <tbody>
                    begin
                    <tr v-if="err">
                        <td>
                            <span> error ...</span>
                        </td>
                    </tr>
                    <!-- <tr v-else-if="load">
                        <td>
                            <span> loading ...</span>
                        </td>
                    </tr> -->
                    <tr v-else v-for="transactions in result" :key="swap.id">
                        <td>
                            <span class="table-body">
                                {{ swap.id }}
                            </span>
                        </td>
                        <td>
                            <span class="table-body">
                                {{ swap.id }}
                            </span>
                        </td>
                        <td>
                            <span class="table-body">
                                {{ swap.id }}
                            </span>
                        </td>
                        <td>
                            <span class="table-body">
                                {{ swap.id }}
                            </span>
                        </td>
                        <td>
                            <span class="table-body">
                                {{ swap.id }}
                            </span>
                        </td>
                        <td>
                            <span class="table-body">
                                {{ swap.id }}
                            </span>
                        </td>
                    </tr>
                    end
                </tbody>
            </table>
        </div>
    </div>
</template>
<script setup>
import gql from 'graphql-tag'
import { useQuery } from '@vue/apollo-composable'
import { onMounted, reactive, ref, toRefs, toRef, unref } from 'vue'
const err = ref(false)
const load = ref(false)
let transactions = reactive({})
let swaps = reactive([])
const QUERY = gql`
query{
 swaps {
   id
  timestamp
  tokenIn
  tokenOut
  userAddress {
    id
  }
  tokenAmountIn
  tokenAmountOut
  tokenInSym
  tokenOutSym
 }
}
`

async function getTransactionFromServer() {
    try {
        const { error, loading, result } = useQuery(QUERY)
        err.value = unref(error)
        load.value =  unref(loading)
        setTimeout(() => {
            transactions = unref(result)
            console.log(err.value, load.value, transactions)
        }, 1000)
    } catch (e) {

        console.log(e)
    }
}
async function getSwaps() {
    if (transactions.swaps) {
        swaps = [...transactions.swaps]
    }
}
onMounted(async () => {
    await getTransactionFromServer()
    await getSwaps()
})


</script>
<style lang="">
    
</style>