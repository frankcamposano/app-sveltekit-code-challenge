<script>
  import Swal from "sweetalert2";

  let users =
    JSON.parse(localStorage.getItem("users"))?.filter((user) => user.active) ||
    [];

  let newUser = {
    user_id: "",
    username: "",
    password: "",
    active: false, 
  };

  function showAlert(title, text, icon) {
    Swal.fire({
      title: title,
      text: text,
      icon: icon,
      confirmButtonText: "Aceptar",
    });
  }

  function isUserAlreadyAdded(username) {
    return users.some((user) => user.username === username);
  }



  function addUser() {
	newUser.username = newUser.username.trim();
    newUser.password = newUser.password.trim();
    if (!newUser.username.trim() || !newUser.password.trim()) {
      showAlert(
        "Advertencia",
        "Por favor, rellena todos los campos antes de agregar al usuario.",
        "warning"
      );
      return;
    }

    // Validar que la contraseña no sea mayor de 10 caracteres
    if (newUser.password.length > 10) {
      showAlert("Error", "La contraseña no puede tener más de 10 caracteres.", "error");
      return;
    }

    if (isUserAlreadyAdded(newUser.username)) {
      showAlert(
        "Advertencia",
        "El nombre de usuario ya ha sido agregado previamente.",
        "warning"
      );
      return;
    }
	

    if (isUserAlreadyAdded(newUser.username)) {
      showAlert(
        "Advertencia",
        "El nombre de usuario ya ha sido agregado previamente.",
        "warning"
      );
      return;
    }

    const lastUserId = users.length > 0 ? users[users.length - 1].user_id : 0;
    const newUserId = lastUserId + 1;

    const userToAdd = { ...newUser, user_id: newUserId };

    users = [...users, { ...userToAdd, user_id: Number(newUserId) }];

    saveToLocalStorage();
    newUser = { user_id: "", username: "", password: "", active: false }; // Establecemos 'active' en 'false' para nuevos usuarios
  }

  function toggleUserStatus(index) {
    users[index].active = !users[index].active;
    saveToLocalStorage();
  }

  function saveToLocalStorage() {
    localStorage.setItem("users", JSON.stringify(users));
  }

  function getUserStatus(username) {
    const user = users.find((user) => user.username === username);
    return user ? (user.active ? "Activo" : "Inactivo") : "No encontrado";
  }
  

  let editedUserId = null;
  let editedUsername = "";
  let editedPassword = "";

  function editUser(userId) {
    const userToEdit = users.find((user) => user.user_id === userId);
    if (userToEdit) {
      editedUserId = userToEdit.user_id;
      editedUsername = userToEdit.username;
      editedPassword = userToEdit.password;
    }
  }

  function saveEditedUser() {
    const index = users.findIndex((user) => user.user_id === editedUserId);
    if (index !== -1) {
      // Validar que la contraseña no sea mayor de 10 caracteres
      if (editedPassword.length > 10) {
        showAlert("Error", "La contraseña no puede tener más de 10 caracteres.", "error");
        return;
      }

      users[index].username = editedUsername;
      users[index].password = editedPassword;
      saveToLocalStorage();
      showAlert("Éxito", "Cambios guardados exitosamente.", "success");
      cancelEdit();
    }
  }

  function cancelEdit() {
    editedUserId = null;
    editedUsername = "";
    editedPassword = "";
  }
</script>

<main class="container">
  <h1>Gestión de Usuarios</h1>

  <form on:submit|preventDefault={addUser}>
    <div class="mb-3">
      <label for="username" class="form-label">Nombre de Usuario:</label>
      <input
        type="text"
        id="username"
        bind:value={newUser.username}
        class="form-control"
      />
    </div>
    <div class="mb-3">
      <label for="password" class="form-label">Contraseña:</label>
      <input
        type="password"
        id="password"
        bind:value={newUser.password}
        class="form-control"
      />
    </div>
    <button type="submit" class="btn btn-primary"> Agregar Usuario </button>
  </form>
  <br /><br /><br />

  <h2>Listado de Usuarios</h2>

  <table class="table">
    <thead class="thead-light">
      <tr>
        <th>ID</th>
        <th>Nombre de Usuario</th>
        <th>Contraseña</th>
        <th>Estado</th>
        <th>Acciones</th>
      </tr>
    </thead>
    <tbody>
      {#each users as user, index}
        <tr>
          <td>{user.user_id}</td>
          <td>{user.username}</td>
          <td>{user.password}</td>
          <td>{getUserStatus(user.username)}</td>
          <td>
            {#if user.active}
              <button
                class="btn btn-danger"
                on:click={() => toggleUserStatus(index)}
              >
                <i class="fas fa-toggle-on" /> Desactivar
              </button>
            {:else}
              <button
                class="btn btn-success"
                on:click={() => toggleUserStatus(index)}
              >
                <i class="fas fa-toggle-off" /> Activar
              </button>
            {/if}
            <button
              class="btn btn-primary"
              on:click={() => editUser(user.user_id)}
            >
              <i class="fas fa-edit" /> Editar
            </button>
            {#if editedUserId === user.user_id}
        <!-- Modal para editar usuario -->
        <div class="modal" style="display: block;">
          <!-- ... (contenido del modal) ... -->
          <div class="modal-dialog modal-dialog-centered">
            <div class="modal-content">
              <div class="modal-header">
                <h5 class="modal-title">Editar Usuario</h5>
                <button type="button" class="close" on:click={cancelEdit}>
                  <span aria-hidden="true">&times;</span>
                </button>
              </div>
              <div class="modal-body">
                <form on:submit|preventDefault={saveEditedUser}>
                  <!-- Campo para editar nombre de usuario -->
                  <div class="mb-3">
                    <label for="edit-username" class="form-label">Nombre de Usuario:</label>
                    <input type="text" id="edit-username" bind:value={editedUsername} class="form-control">
                  </div>
                  <!-- Campo para editar contraseña -->
                  <div class="mb-3">
                    <label for="edit-password" class="form-label">Contraseña:</label>
                    <input type="password" id="edit-password" bind:value={editedPassword} class="form-control">
                  </div>
                  <button type="submit" class="btn btn-primary">Guardar Cambios</button>
                  <button type="button" class="btn btn-secondary" on:click={cancelEdit}>Cancelar</button>
                </form>
              </div>
            </div>
          </div>
        </div>
        <div class="modal-backdrop" style="z-index: 1040; background-color: rgba(255, 255, 255, 0.5);"></div> 
{/if}
          </td>
        </tr>
      {/each}
    </tbody>
  </table>
</main>

<style>
  @import "./node_modules/@fortawesome/fontawesome-free/css/all.css";
</style>
