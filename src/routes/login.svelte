<script>
  import { goto } from "$app/navigation";
  import supabase from "$lib/db";
  import { user } from "$lib/stores";

  let email = "";
  let isNewRegistration = false;

  const signUp = async () => {
    let { user: userDetails, error } = await supabase.auth.signUp({
      email: email,
      password: "DZMfuXtrtWmPLKFFhLss",
    });
    $user = userDetails;
    goto("/");
  };

  const logIn = async () => {
    let { user: userDetails, error } = await supabase.auth.signIn({
      email: email,
      password: "DZMfuXtrtWmPLKFFhLss",
    });
    $user = userDetails;
    goto("/");
  };
</script>

{#if $user.email}
  <p>You're already logged in.</p>
{:else}
  <label for=""
    >Email: <input
      bind:value={email}
      type="email"
      placeholder="youremail@email.com"
    /></label
  >
  {#if isNewRegistration}
    <button on:click={signUp}> SignUp </button>
    <p class="switch" on:click={() => (isNewRegistration = false)}>
      Already have an account?
    </p>
  {:else}
    <button on:click={logIn}> Login </button>
    <p class="switch" on:click={() => (isNewRegistration = true)}>
      Create a new account
    </p>
  {/if}
{/if}
