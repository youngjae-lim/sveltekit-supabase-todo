<script>
  import { goto } from "$app/navigation";
  import supabase from "$lib/db";
  import { user } from "$lib/stores";

  let email = "";
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

<label for=""
  >Email: <input
    bind:value={email}
    type="email"
    placeholder="youremail@email.com"
  /></label
>
<button on:click={signUp}> SignUp </button>
<button on:click={logIn}> Login </button>
