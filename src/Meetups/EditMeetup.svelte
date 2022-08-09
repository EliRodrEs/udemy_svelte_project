<script>
  import TextInput from "../UI/TextInput.svelte"
  import Button from "../UI/Button.svelte"

  import { createEventDispatcher } from 'svelte'

  let title = ''
  let subtitle = ''
  let address = ''
  let description = ''
  let imageUrl = ''
  let email = ''
  const dispatch = createEventDispatcher()

  function submitForm() {
    dispatch('save', {
      title: title,
      subtitle: subtitle,
      address: address,
      description: description,
      imageUrl: imageUrl,
      email: email
    })
  }

</script>

<form on:submit|preventDefault={submitForm}>
  <TextInput controlType="text" id="title" label="Title" value={title} on:input={event => (title = event.target.value)} />
  <TextInput controlType="text" id="subtitle" label="Subtitle" value={subtitle} on:input={event => (subtitle = event.target.value)} />
  <TextInput controlType="text" id="address" label="Address" value={address} on:input={event => (address = event.target.value)} />
  <TextInput controlType="text" id="imageUrl" label="Image URL" value={imageUrl} on:input={event => (imageUrl = event.target.value)} />
  <TextInput controlType="email" id="email" label="Email" value={email} on:input={event => (email = event.target.value)} />
  <TextInput id="description" controlType="textarea" rows="3" label="Description" value={description} on:input={event => (description = event.target.value)} />
  <Button type="submit" caption="Save" />
</form>

<style>
  form {
    width: 30rem;
    max-width: 90%;
    margin: auto;
  }
</style>