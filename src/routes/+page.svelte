<script>
    import { marked } from 'marked';
    let value = `# Heading level 1\n## Heading level 2\n### Heading level 3\n\nThis is a paragraph, some words can be *italic* and some can be **bold**\n\nIf you want a list:\n- you\n- can\n- add it\n- here`;
</script>

<div id="container">
    <div>
        <h3>
            Editor de Markdown
        </h3>
        <p>
            Escribe texto markdown y ve el resultado en tiempo real.
        </p>
    </div>
    <div id="editor">
        Markdown
        <textarea bind:value={value} cols="60" rows="20"></textarea>
    </div>
    <div id="preview">
        Resultado
        <div class="content">
            {@html marked(value)}
        </div>
    </div>
</div>

<style>
    #container {
        font-size: 16px;
        font-family: system-ui, "Segoe UI", Roboto, Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";        width: 100%;
        display: flex;
        height: 100vh;
        background: rgb(254, 243, 227);
        gap: 1rem;
        padding: 1rem;
        box-sizing: border-box;
    }
    #editor, #preview {
        display: block;
        width: 50%;
    }
    #editor {
        border-radius: 7px;
    }
    textarea {
        width: 100%;
        height: 60%;
        resize: none;
        box-sizing: border-box;
        background: white;
        padding: 1rem;
        border-radius: 6px;
        border: 1px solid rgb(225, 225, 225);
        font-size: 1rem;
        line-height: 1.4rem;
    }
    .content {
        border-radius: 7px;
        background: rgb(15, 29, 41);
        height: 60%;
        padding: 1rem;
        box-sizing: border-box;
        color: rgb(219, 219, 219);
        line-height: 2rem;
        overflow-y: scroll;
    }
</style>
