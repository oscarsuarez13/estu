# estu
laboratorio 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(to bottom, #a2c4fc, #f9f7fd);
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .login-container {
            background: white;
            padding: 2rem;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            width: 300px;
            text-align: center;
        }
        .login-container h1 {
            margin-bottom: 1.5rem;
            color: #333;
        }
        .login-container input {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        .login-container button {
            width: 100%;
            padding: 10px;
            background-color: #4CAF50;
            border: none;
            color: white;
            font-size: 16px;
            cursor: pointer;
            border-radius: 4px;
        }
        .login-container button:hover {
            background-color: #45a049;
        }
        .login-container a {
            display: block;
            margin-top: 10px;
            color: #007BFF;
            text-decoration: none;
        }
        .login-container a:hover {
            text-decoration: underline;
        }

        /* Modal Styling */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            justify-content: center;
            align-items: center;
        }
        .modal-content {
            background: white;
            padding: 2rem;
            border-radius: 8px;
            text-align: center;
            width: 350px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
        }
        .modal-content h2 {
            margin-bottom: 1rem;
            color: #333;
        }
        .modal-content input {
            width: 100%;
            padding: 8px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        .modal-content button {
            padding: 10px;
            width: 100%;
            background-color: #007BFF;
            color: white;
            border: none;
            border-radius: 4px;
            font-size: 16px;
            cursor: pointer;
        }
        .modal-content button:hover {
            background-color: #0056b3;
        }
        .close {
            color: red;
            float: right;
            font-size: 20px;
            font-weight: bold;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="login-container">
        <h1>Iniciar Sesión</h1>
        <form action="/login" method="POST">
            <input type="text" name="username" placeholder="Usuario" required>
            <input type="password" name="password" placeholder="Contraseña" required>
            <button type="submit">Entrar</button>
        </form>
        <a href="#" id="registerLink">¿No tienes cuenta? Regístrate</a>
        <a href="#" id="resetPasswordLink">¿Olvidaste tu contraseña?</a>
    </div>

    <!-- Modal para registro -->
    <div class="modal" id="registerModal">
        <div class="modal-content">
            <span class="close" id="closeModal">&times;</span>
            <h2>Registro</h2>
            <form action="/register" method="POST">
                <table>
                    <tr>
                        <td><label for="lastName">Apellidos:</label></td>
                        <td><input type="text" id="lastName" name="lastName" placeholder="Apellidos" required></td>
                    </tr>
                    <tr>
                        <td><label for="firstName">Nombres:</label></td>
                        <td><input type="text" id="firstName" name="firstName" placeholder="Nombres" required></td>
                    </tr>
                    <tr>
                        <td><label for="email">Correo:</label></td>
                        <td><input type="email" id="email" name="email" placeholder="Correo Electrónico" required></td>
                    </tr>
                    <tr>
                        <td><label for="code">Código:</label></td>
                        <td><input type="text" id="code" name="code" placeholder="Código" required></td>
                    </tr>
                    <tr>
                        <td><label for="grade">Grado:</label></td>
                        <td><input type="text" id="grade" name="grade" placeholder="Grado" required></td>
                    </tr>
                </table>
                <button type="submit">Registrarse</button>
            </form>
        </div>
    </div>

    <!-- Modal para recuperación de contraseña -->
    <div class="modal" id="resetPasswordModal">
        <div class="modal-content">
            <span class="close" id="closeResetModal">&times;</span>
            <h2>Recuperar Contraseña</h2>
            <form action="/reset_password" method="POST" id="resetForm">
                <label for="resetEmail">Correo electrónico:</label>
                <input type="email" id="resetEmail" name="resetEmail" placeholder="Correo electrónico" required>
                <label for="resetCode">Código:</label>
                <input type="text" id="resetCode" name="resetCode" placeholder="Código" required>
                <button type="submit">Enviar</button>
            </form>
        </div>
    </div>

    <script>
        // Modal Handling
        const registerLink = document.getElementById('registerLink');
        const registerModal = document.getElementById('registerModal');
        const closeModal = document.getElementById('closeModal');
        const resetPasswordLink = document.getElementById('resetPasswordLink');
        const resetPasswordModal = document.getElementById('resetPasswordModal');
        const closeResetModal = document.getElementById('closeResetModal');

        // Open Modal for Registration
        registerLink.addEventListener('click', (e) => {
            e.preventDefault();
            registerModal.style.display = 'flex';
        });

        // Open Modal for Reset Password
        resetPasswordLink.addEventListener('click', (e) => {
            e.preventDefault();
            resetPasswordModal.style.display = 'flex';
        });

        // Close Modal for Registration
        closeModal.addEventListener('click', () => {
            registerModal.style.display = 'none';
        });

        // Close Modal for Reset Password
        closeResetModal.addEventListener('click', () => {
            resetPasswordModal.style.display = 'none';
        });

        // Close Modal on Outside Click
        window.addEventListener('click', (e) => {
            if (e.target === registerModal) {
                registerModal.style.display = 'none';
            }
            if (e.target === resetPasswordModal) {
                resetPasswordModal.style.display = 'none';
            }
        });

        // Send the reset password data (you need server-side code for this)
        const resetForm = document.getElementById('resetForm');
        resetForm.addEventListener('submit', (e) => {
            e.preventDefault();

            const resetEmail = document.getElementById('resetEmail').value;
            const resetCode = document.getElementById('resetCode').value;

            // Sending email (replace this part with a real email sending API or backend code)
            fetch('/send_reset_email', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ email: resetEmail, code: resetCode })
            })
            .then(response => response.json())
            .then(data => {
                alert('Correo enviado con éxito');
                resetPasswordModal.style.display = 'none';
            })
            .catch(error => {
                console.error('Error:', error);
                alert('Hubo un problema al enviar el correo');
            });
        });
    </script>
</body>
</html>
