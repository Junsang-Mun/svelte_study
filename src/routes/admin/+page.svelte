<script>
	// @ts-nocheck
	import { onMount } from 'svelte';
	import Editor from '@toast-ui/editor';
	import '@toast-ui/editor/dist/toastui-editor.css';
	import '@toast-ui/editor/dist/theme/toastui-editor-dark.css';
	let texteditor, toastEditor;
	let currentDate = new Date();
	const offset = currentDate.getTimezoneOffset();
	currentDate = new Date(currentDate.getTime() - (offset * 60 * 1000));
	let pTitle, pCategory, pDate = currentDate.toISOString().split('T')[0];

	onMount(() => {
		toastEditor = new Editor({
			el: texteditor,
			height: '800px',
			initialEditType: 'markdown',
			previewStyle: 'vertical',
			theme: 'dark',
		})
	})

	function submitNewPost() {
		console.log(`${pTitle}\n${pCategory}\n${pDate}`);
		console.log(toastEditor.getHTML());
	}
</script>

<h1>글 쓰기</h1>
<input type="text" placeholder="제목" class="form" bind:value={pTitle}>
<input type="text" placeholder="카테고리" class="form" bind:value={pCategory}>
<input type="date" placeholder="작성일" class="form" bind:value={pDate}>
<div bind:this={texteditor}></div>
<br>
<button on:click={() => submitNewPost()} class="formsub">저장하기</button>
