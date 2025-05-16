<!-- 특정 행위로 인해 자동으로 알림이 갔을 때 
 response가 올때까지 기다리는 화면 -->
<script lang="ts">
  export let isVisible: boolean = false;
  export let message: string = "로딩 중...";
</script>

<style>
    @import '../css/loadingScreen.css';
</style>


{#if isVisible}
  <div class="modal-backdrop">
    <div class="loading-modal">
      <div class="spinner"></div>
      <p>{message}</p>
    </div>
  </div>
{/if}