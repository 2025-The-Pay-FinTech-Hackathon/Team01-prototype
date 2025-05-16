<script lang="ts">
    import { onMount } from 'svelte'

    interface Agent {
        name: String,
        phonenumber: String,
    }

    let agentList: Agent[] = [];
    let inputname: string = '';
    let inputphone: string = '';

    // component가 browser에 mount된다음 실행되는 코드
    onMount(() => {
        //(TODO) tiny-db Search query && update agentList
        
    })

    //대리인 등록
    function registerAgent(): void {
        const trimmedName = inputname.trim();
        const trimmedPhone = inputphone.trim();
        if (trimmedName === '' || trimmedPhone === '') {
            alert('이름과 전화번호를 입력하세요.');
            return;
        }

        agentList = [...agentList, {
            name: trimmedName,
            phonenumber: trimmedPhone,
        }];
        inputname = '';
        inputphone = '';

        //(TODO) tiny-db insert query
    }
</script>

<div style="margin: 30px auto 0; text-align: center">
    <input bind:value={inputname} placeholder="대리인 이름 입력" />
    <input bind:value={inputphone} placeholder="전화번호 입력"/>
    <button on:click={registerAgent}>등록</button>
</div>


<div style="margin: 30px auto 0; text-align: center">
    <ul>
    {#each agentList as agent, index}
        <li>{index + 1}. 이름: {agent.name} , 전화: {agent.phonenumber}</li>
    {/each}
    </ul>
</div>
