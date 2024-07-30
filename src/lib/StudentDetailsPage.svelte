<script>
    import axios from 'axios';
    import {onMount} from 'svelte';
    import {
        Button, Drawer, Input,
        Table,
        TableBody,
        TableBodyCell,
        TableBodyRow,
        TableHead,
        TableHeadCell,
        TableSearch
    } from 'flowbite-svelte';
    import StudentEnrollementForm from "./StudentEnrollementForm.svelte";
    import { sineIn } from 'svelte/easing';

    let searchTerm = '';
    let items = [
        {id: 1, firstName: 'Shanaya', lastName: 'Karuneegar', age: 8, gender: "FEMALE"},
        {id: 2, firstName: 'Saathvi', lastName: 'Venkatesh', age: 8, gender: "FEMALE"},
        {id: 3, firstName: 'Saanvi', lastName: 'Mohan', age: 11, gender: "FEMALE"},
        {id: 4, firstName: 'Krithi', lastName: 'Gandhi', age: 8, gender: "FEMALE"}
    ];

    let backedItems ;
    onMount(async () => {
        const itemx = await axios.get("http://localhost:8080/v1/students"); // Make the API Call here
        console.log(itemx.data)
        items = itemx.data
        backedItems = itemx.data
    });


    $: filteredItems = items.filter((item) => item.firstName.toLowerCase().indexOf(searchTerm.toLowerCase()) !== -1);


    let hidden6 = true;
    let selectedItem ;
    let newSelectItem ={
        firstName: '',
        lastName: '',
        age: ''
    }
    let transitionParamsRight = {
        x: 320,
        duration: 200,
        easing: sineIn
    };
</script>

<div class="h-svh relative w-full" >
    <div class="mb-6 absolute top-0 right-0">
        <Button on:click={() => {hidden6 = false; selectedItem = newSelectItem}}>ADD STUDENT</Button>
    </div>
    <Table divClass="" bind:value={items}>
        <TableHead>
            <TableHeadCell>ID</TableHeadCell>
            <TableHeadCell>FIRST NAME</TableHeadCell>
            <TableHeadCell>LAST NAME</TableHeadCell>
            <TableHeadCell>AGE</TableHeadCell>
            <TableHeadCell>GENDER</TableHeadCell>
        </TableHead>
        <TableBody tableBodyClass="divide-y" >
            {#each filteredItems as item}
                <TableBodyRow>
                    <TableBodyCell>{item.id}</TableBodyCell>
                    <TableBodyCell>{item.firstName}</TableBodyCell>
                    <TableBodyCell>{item.lastName}</TableBodyCell>
                    <TableBodyCell>{item.age}</TableBodyCell>
                    <TableBodyCell>{item.gender}</TableBodyCell>
                    <TableBodyCell><Button id="{item.id}" color="alternative" on:click={() => {hidden6 = false; selectedItem = item}}>EDIT</Button></TableBodyCell>
                </TableBodyRow>
            {/each}
        </TableBody>
    </Table>

    <Drawer placement="right" transitionType="fly" transitionParams={transitionParamsRight} bind:hidden={hidden6} id="sidebar6" class="w-6/12">
        <StudentEnrollementForm
                firstName="{selectedItem.firstName}"
                lastName="{selectedItem.lastName}"
                id="{selectedItem.id}"
                age={selectedItem.age}
                selectedGender="{selectedItem.gender}"
                clearFunc="{() => (hidden6 = true)}"
        ></StudentEnrollementForm>
    </Drawer>
</div>