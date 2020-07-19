# Step to develop

### 1. Create Login component

```
$ng generate component login
$ng g c login

CREATE src/app/login/login.component.css (0 bytes)
CREATE src/app/login/login.component.html (20 bytes)
CREATE src/app/login/login.component.spec.ts (621 bytes)
CREATE src/app/login/login.component.ts (271 bytes)
UPDATE src/app/app.module.ts (471 bytes)

$ng generate component --flat login
```

Generate component without a new directory

```
$ng generate component --flat login
```

### 2. Using [bootstrap css](https://getbootstrap.com/)

Edit file index.html

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>HelloApp</title>
    <base href="/" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <link rel="icon" type="image/x-icon" href="favicon.ico" />

    <link
      rel="stylesheet"
      href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css"
      integrity="sha384-9aIt2nRpC12Uk9gS9baDl411NQApFmC26EwAOH8WgZl5MYYxFfc+NcPb1dKGj7Sk"
      crossorigin="anonymous"
    />
  </head>
  <body>
    <app-root>Loading ...</app-root>
  </body>
</html>

```

### 3. Create login form of Login component

/login/login.component.html

```
<h2>Login</h2>
<form>
  <div class="form-group">
    <label for="username">Username</label>
    <input type="text" formControlName="username" class="form-control" />
  </div>
  <div class="form-group">
    <label for="password">Password</label>
    <input type="password" formControlName="password" class="form-control" />
  </div>
  <div class="form-group">
    <button class="btn btn-primary">
      Login
    </button>
    <a routerLink="/register" class="btn btn-link">Register</a>
  </div>
</form>
```

### Quiz

Try to show login form in browser !!

### 4. Add /login to App router

Edit file `app-routing.modules.ts`

```
import { LoginComponent } from './login/login.component';

const routes: Routes = [{ path: 'login', component: LoginComponent }];

```

Edit file `app.component.html`

```
<!-- nav -->
<nav class="navbar navbar-expand navbar-dark bg-dark">
  <div class="navbar-nav">
    <a class="nav-item nav-link" routerLink="/">Home</a>
    <a class="nav-item nav-link">Logout</a>
  </div>
</nav>

<!-- main -->
<div class="jumbotron">
  <div class="container">
    <div class="row">
      <div class="col-sm-6 offset-sm-3">
        <router-outlet></router-outlet>
      </div>
    </div>
  </div>
</div>

```

See result in web browser `http://localhost:4200/login`
