<script lang="ts">
    import { onMount } from 'svelte'

    interface Author {
        name: String,
        kakaoemail: String,
    }

    let agentList: Author[] = [];
    let inputname: string = '';
    let inputkakaoemail: string = '';

    // component가 browser에 mount된다음 실행되는 코드
    onMount(async () => {
        //tiny-db Search query && update agentList
        try {
            const res = await fetch("http://127.0.0.1:8000/searchAuthor", {
                method: "GET",
                headers: { 'Content-Type': 'application/json' },
            })
            if (!res.ok)
                throw new Error('db에서 불러오기 실패');
            let result = await res.json()
            result.data.map((data: Author) => {
                agentList = [...agentList, data]
            })
        } catch (err) {
            console.error("searchAuthor 에러: ", err);
        }
    })

    //대리인 등록
    async function registerAgent(): Promise<void> {
        const trimmedName = inputname.trim();
        const trimmedEmail = inputkakaoemail.trim();
        if (trimmedName === '' || trimmedEmail === '') {
            alert('이름과 전화번호를 입력하세요.');
            return;
        }

        const insertData = {
            name: trimmedName,
            kakaoemail: trimmedEmail,
        }
        agentList = [...agentList, insertData];
        inputname = '';
        inputkakaoemail = '';

        //tiny-db insert query
        try {
            const res = await fetch("http://127.0.0.1:8000/insertAuthor", {
                method: "POST",
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(insertData)
            })
            if (!res.ok) {
                throw new Error('db에 Author 저장 실패')
            }
        } catch (err) {
            console.error("insertAuthor 에러: ", err);
        }
    }
</script>

<div style="margin: 30px auto 0; text-align: center">
    <input bind:value={inputname} placeholder="대리인 이름 입력" />
    <input bind:value={inputkakaoemail} placeholder="카카오이메일 입력"/>
    <button on:click={registerAgent}>등록</button>
</div>


<div style="margin: 30px auto 0; text-align: center">
    <ul>
    {#each agentList as agent, index}
        <li>{index + 1}. 이름: {agent.name}  ,  카카오이메일: {agent.kakaoemail} </li>
    {/each}
    </ul>
</div>
