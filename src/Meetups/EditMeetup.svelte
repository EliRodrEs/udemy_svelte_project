<script>
  import TextInput from "../UI/TextInput.svelte"
  import Button from "../UI/Button.svelte"
  import Modal from "../UI/Modal.svelte"
  import { isEmpty } from "../helpers/validation"

  import { createEventDispatcher } from "svelte"

  let title = ""
  let titleValid = false;
  let subtitle = ""
  let address = ""
  let description = ""
  let imageUrl = ""
  let email = ""
  const dispatch = createEventDispatcher()

  $: titleValid = !isEmpty(title)

  function submitForm() {
    dispatch("save", {
      title: title,
      subtitle: subtitle,
      address: address,
      description: description,
      imageUrl: imageUrl,
      email: email,
    })
  }

  function cancel() {
    dispatch("cancel")
  }
</script>

<Modal title="Edit Meetup Data" on:cancel>
  <form on:submit|preventDefault={submitForm}>
    <TextInput
      controlType="text"
      id="title"
      label="Title"
      valid={titleValid}
      validityMessage="Please enter a valid title."
      value={title}
      on:input={(event) => (title = event.target.value)}
    />
    <TextInput
      controlType="text"
      id="subtitle"
      label="Subtitle"
      value={subtitle}
      on:input={(event) => (subtitle = event.target.value)}
    />
    <TextInput
      controlType="text"
      id="address"
      label="Address"
      value={address}
      on:input={(event) => (address = event.target.value)}
    />
    <TextInput
      controlType="text"
      id="imageUrl"
      label="Image URL"
      value={imageUrl}
      on:input={(event) => (imageUrl = event.target.value)}
    />
    <TextInput
      controlType="email"
      id="email"
      label="Email"
      value={email}
      on:input={(event) => (email = event.target.value)}
    />
    <TextInput
      id="description"
      controlType="textarea"
      rows="3"
      label="Description"
      value={description}
      on:input={(event) => (description = event.target.value)}
    />
  </form>
  <div slot="footer">
    <Button type="button" mode="outline" on:click={cancel}>Cancel</Button>
    <Button type="button" on:click={submitForm}>Save</Button>
  </div>
</Modal>

<style>
  form {
    width: 100%;
  }
</style>
