<script>
    import axios from 'axios';
    import {Input, Label, Button, Select, Card} from 'flowbite-svelte';

    export let selectedGender = '';
    let gender = [
        {value: 'MALE', name: 'MALE'},
        {value: 'FEMALE', name: 'FEMALE'}
    ]

    export let id = '';
    export let firstName = '';
    export let lastName = '';
    export let age = 0;

    export let clearFunc;

    async function doPost() {
        let students ={
            id: id,
            firstName: firstName,
            lastName: lastName,
            age: parseInt(age),
            gender: selectedGender,
        }
        console.log(JSON.stringify(students));
        const res = await axios.post('http://localhost:8080/v1/students', students)
        console.log(JSON.stringify(res.data))
    }
</script>

<div class="container content-center">
    <Card class="text-left content-end" size="lg" padding="xl">
        <div class="mb-6">
            <Label for="first_name" class="mb-2">First name</Label>
            <Input type="text" id="first_name" placeholder="John" bind:value={firstName} required/>
        </div>
        <div class="mb-6">
            <Label for="last_name" class="mb-2">Last name</Label>
            <Input type="text" id="last_name" placeholder="Doe" bind:value={lastName} required/>
        </div>
        <div class="mb-6">
            <Label for="sex" class="mb-2">Gender</Label>
            <Select class="mt-2" items={gender} bind:value={selectedGender}/>
        </div>
        <div class="mb-6">
            <Label for="age" class="mb-2">Age</Label>
            <Input type="number" id="age" placeholder="1-10" pattern={"[0-1]{2}"} bind:value={age} required/>
        </div>
        <div class="mb-6 align-middle flex-row-reverse">
            <Button color="alternative" size="sm" on:click={clearFunc} >CLEAR</Button>
            <Button type="submit" size="sm" on:click={doPost} >SUBMIT</Button>
        </div>
    </Card>
</div>