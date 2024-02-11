<script>
    import { marked } from 'marked';

    let editorValue = `# Heading level 1\n## Heading level 2\n### Heading level 3\n\nThis is a paragraph, some words can be *italic* and some can be **bold**\n\nIf you want a list:\n- you\n- can\n- add it\n- here`;
    let fileName = 'filename.txt';
    $: canSave = fileName !== '' && editorValue !== '';

    function update() {
        let tempLink = document.createElement('a');
        let blob = new Blob([editorValue], { type: 'text/plain' });

        tempLink.setAttribute('href', URL.createObjectURL(blob));
        tempLink.setAttribute('download', fileName);
        tempLink.click();

        URL.revokeObjectURL(tempLink.href);
    }
</script>

<svelte:document />

<div class="panel">
    <div id="save">
        <h3>
            Editor de Markdown
        </h3>
        <p>
            Escribe texto markdown y ve el resultado en tiempo real.
        </p>
        <input type="text" bind:value={fileName}>
        <button on:click={update} disabled={!canSave}>
            Guardar
        </button>
        {#if !canSave}
            <p class="validation">
                Algunos campos son requeridos.
            </p>
        {/if}
    </div>
    <div id="editor">
        <textarea bind:value={editorValue} cols="60" rows="20"></textarea>
    </div>
    <div id="preview">
        <span>
            {@html marked(editorValue)}
        </span>
    </div>
</div>

<style>
    .panel {
        font-size: 16px;
        font-family: system-ui, "Segoe UI", Roboto, Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";        width: 100%;
        display: flex;
        flex-direction: column;
        height: 100vh;
        background: rgb(255, 234, 234);
        gap: 1rem;
        padding: 1rem;
        box-sizing: border-box;
    }

    #save input {
        border: 1px solid rgb(214, 214, 214);
        padding: 0.3rem;
        color: rgb(22, 22, 22);
        border-radius: 4px;
        font-size: 1rem;
    }
    #save button {
        background: rgb(197, 91, 213);
        padding: 0.3rem 1rem;
        border: none;
        border-radius: 4px;
        font-size: 1rem;
        color: white;
    }
    #save button:hover {
        cursor: pointer;
    }
    #save button:disabled {
        cursor: not-allowed;
        background: grey;
    }
    #save .validation {
        color: red;
    }
    #editor, #preview {
        width: 100%;
        border-radius: 7px;
    }
    #editor textarea {
        width: 100%;
        resize: none;
        box-sizing: border-box;
        background: white;
        padding: 1rem;
        border-radius: 6px;
        border: 1px solid rgb(225, 225, 225);
        font-size: 1rem;
        line-height: 1.4rem;
    }
    #preview span {
        display: block;
        border-radius: 7px;
        background: rgb(47, 52, 67);
        padding: 1rem;
        box-sizing: border-box;
        color: rgb(219, 219, 219);
        line-height: 2rem;
        overflow-y: scroll;
    }
    @media screen and (min-width: 768px) {
        .panel {
            flex-direction: row;
        }
        #editor, #preview {
            display: block;
            width: 50%;
            border-radius: 7px;
        }
        #editor textarea {
            height: 60%;
        }
    }
</style>
