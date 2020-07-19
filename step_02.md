# Step to develop

### 1. Submit form

Edit file /login/login.component.html

```
<h2>Login</h2>
<form [formGroup]="loginForm" (ngSubmit)="onSubmit()">
...
</form>

```

Edit file /login/login.component.ts

```
import { Component, OnInit } from '@angular/core';
import { FormBuilder, FormGroup } from '@angular/forms';
@Component({
  selector: 'app-login',
  templateUrl: './login.component.html',
  styleUrls: ['./login.component.css'],
})
export class LoginComponent implements OnInit {
  loginForm: FormGroup;
  constructor(private formBuilder: FormBuilder) {}

  ngOnInit(): void {
    this.loginForm = this.formBuilder.group({
      username: [''],
      password: [''],
    });
  }

  onSubmit(): void {
    console.log('onSubmit');
    console.log(this.loginForm.controls.username.value);
    console.log(this.loginForm.controls.password.value);
  }
}
```

Enable ReactiveForm module in file app.module.ts

```
@NgModule({
  declarations: [AppComponent, LoginComponent],
  imports: [BrowserModule, AppRoutingModule, ReactiveFormsModule],
  providers: [],
  bootstrap: [AppComponent],
})
```

### 2. Validate data in form

Edit file /login/login.component.ts

```
import { Validators } from '@angular/forms';

export class LoginComponent implements OnInit {
  ...
  ngOnInit(): void {
    this.loginForm = this.formBuilder.group({
      username: ['', Validators.required],
      password: ['', Validators.required],
    });
  }

  onSubmit(): void {
    ...
    if (this.loginForm.invalid) {
      return;
    }
  }
}

```

Edit file /login/login.component.html

```
<h2>Login</h2>
<form [formGroup]="loginForm" (ngSubmit)="onSubmit()">
  <div class="form-group">
    <label for="username">Username</label>
    <input
      type="text"
      formControlName="username"
      class="form-control"
      [ngClass]="{ 'is-invalid': loginForm.controls.username.errors }"
    />
    <div *ngIf="loginForm.controls.username.errors" class="invalid-feedback">
      <div *ngIf="loginForm.controls.username.errors.required">
        Username is required
      </div>
    </div>
  </div>
  <div class="form-group">
    <label for="password">Password</label>
    <input
      type="password"
      formControlName="password"
      class="form-control"
      [ngClass]="{ 'is-invalid': loginForm.controls.password.errors }"
    />
    <div *ngIf="loginForm.controls.password.errors" class="invalid-feedback">
      <div *ngIf="loginForm.controls.password.errors.required">
        Password is required
      </div>
    </div>
  </div>
  <div class="form-group">
    <button class="btn btn-primary">
      Login
    </button>
    <a routerLink="/register" class="btn btn-link">Register</a>
  </div>
</form>
```

## Quiz :: ไม่แสดง vaalidation message ในการเข้ามาหน้า login ครั้งแรก ?
