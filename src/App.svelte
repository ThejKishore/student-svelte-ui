<script>
  import StudentEnrollementForm from "./lib/StudentEnrollementForm.svelte";
  import {TabItem, Tabs} from "flowbite-svelte";
  import StudentDetailsPage from "./lib/StudentDetailsPage.svelte";

  let selectedItem ={
    firstName: '',
    lastName: '',
    age: ''
  }
  const clearItem = {
    firstName: '',
    lastName: '',
    age: ''
  }

</script>

<main>
  <Tabs tabStyle="underline" selectedTabStyle="dark:bg-gray-800" >
    <TabItem open title="Student List" >
      <StudentDetailsPage></StudentDetailsPage>
    </TabItem>
    <TabItem title="Student Form">
      <StudentEnrollementForm
              firstName="{selectedItem.firstName}"
              lastName="{selectedItem.lastName}"
              id="{selectedItem.id}"
              age={selectedItem.age}
              selectedGender="{selectedItem.gender}"
              clearFunc="{() => (selectedItem = clearItem)}"
      ></StudentEnrollementForm>
    </TabItem>
  </Tabs>
</main>

<style global lang="postcss">
  @tailwind utilities;
  @tailwind components;
  @tailwind base;
</style>
