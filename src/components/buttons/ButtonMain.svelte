<script>
    export let label;
    export let url;

    
</script>

<style>
    a {
        display: inline-block;
        background-color: var(--black-100);
        color: white;
        padding: 16px 24px;
        border-radius: 6px;
        text-decoration: none;
        margin: 0 auto;
    }
</style>

<a href={url}>{label}</a>