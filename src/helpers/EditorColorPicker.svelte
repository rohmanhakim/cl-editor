<div style="display: {show ? 'block' : 'none'}">
    <div class="color-picker-overlay" on:click="{close}"></div>
    <div class="color-picker-wrapper">
        {#each btns as btn}
        <button type="button" class="color-picker-btn" style="background-color:{btn.color};" on:click="{event => selectColor(btn)}">{btn.text || ''}</button>
        {/each}
    </div>
</div>

<script>
    import {onMount, createEventDispatcher } from "svelte";

    let dispatcher = new createEventDispatcher();

    const colors = ['ffffff', '000000', 'eeece1', '1f497d', '4f81bd', 'c0504d', '9bbb59', '8064a2', '4bacc6', 'f79646', 'ffff00', 'f2f2f2', '7f7f7f', 'ddd9c3', 'c6d9f0', 'dbe5f1', 'f2dcdb', 'ebf1dd', 'e5e0ec', 'dbeef3', 'fdeada', 'fff2ca', 'd8d8d8', '595959', 'c4bd97', '8db3e2', 'b8cce4', 'e5b9b7', 'd7e3bc', 'ccc1d9', 'b7dde8', 'fbd5b5', 'ffe694', 'bfbfbf', '3f3f3f', '938953', '548dd4', '95b3d7', 'd99694', 'c3d69b', 'b2a2c7', 'b7dde8', 'fac08f', 'f2c314', 'a5a5a5', '262626', '494429', '17365d', '366092', '953734', '76923c', '5f497a', '92cddc', 'e36c09', 'c09100', '7f7f7f', '0c0c0c', '1d1b10', '0f243e', '244061', '632423', '4f6128', '3f3151', '31859b', '974806', '7f6000']

    const getBtns = () => {
        const btns = colors.map((color) => ({ color: `#${color}` }));
        btns.push({ text: '#', modal: true });
        return btns;
    }

    export let show = false;
    export let btns = [];
    export let event = '';

    onMount(()=>{
        btns = getBtns();
    });

    function close() {
        show = false;
    }
    function selectColor(btn) {
        dispatcher(event,btn)
        close();
    }

</script>

<style>
    .color-picker-wrapper {
        border: 1px solid #ecf0f1;
        border-top: none;
        background: #FFF;
        box-shadow: rgba(0,0,0,.1) 0 2px 3px;
        width: 290px;
        left: 50%;
        -webkit-transform: translateX(-50%);
        transform: translateX(-50%);
        padding: 0;
        position: absolute;
        top: 37px;
        z-index: 11;
    }

    .color-picker-overlay {
        position: absolute;
        background-color: rgba(255,255,255,.5);
        height: 100%;
        width: 100%;
        left: 0;
        top: 0;
        z-index: 10;
    }

    .color-picker-btn {
        display: block;
        position: relative;
        float: left;
        height: 20px;
        width: 20px;
        border: 1px solid #333;
        padding: 0;
        margin: 2px;
        line-height: 35px;
        text-decoration: none;
        background: #FFF;
        color: #333!important;
        cursor: pointer;
        text-align: left;
        font-size: 15px;
        transition: all 150ms;
        line-height: 20px;
        padding: 0px 5px;
    }

    .color-picker-btn:hover::after {
        content: " ";
        display: block;
        position: absolute;
        top: -5px;
        left: -5px;
        height: 27px;
        width: 27px;
        background: inherit;
        border: 1px solid #FFF;
        box-shadow: #000 0 0 2px;
        z-index: 10;
    }
</style>
