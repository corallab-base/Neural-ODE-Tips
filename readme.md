# Tips for Training Neural ODE

## 1. Modules

### odeint vs ode_adjoint_int
If you have enough DRAM, head to ODEINT as it's MUCH faster than Adjoint, which has depth-invariant DRAM usage

### Fixed-step vs Adaptive-step odesolver
Fixed-step odesolver is generally faster than adaptive-step, but it's accuracy is worse. Regarding rtol and atol, my recommend value is 1e-3 and 1e-4

### torchdiffeq vs torchdyn
torchdiffeq has the best compatibility and most odesolver options. torchdyn is a little bit faster but sometimes it causes loss.backward() freeze. I recommend torchdiffeq

### Setting combos
1. Balanced speed and accuracy: **odeint, dopri5, and sufficient DRAM**
2. I just need speed: **odeint, any fixed step odesolver (rk, euler, etc)**
3. Limited DRAM: **ode_adjoint_int, fixed step odesolver**

*I personlly recommend setting 1*

## 2. Trainings:

### Behavior
Based on the experience of training poses, Neural-ODE based method tends to learn the spatial feature first and then the temporal feature. With generic RNN embeddings, the model converges slowly. So the tip is wait at least 10 epochs to determine the feasibility of the model.

### Mini-batch
Neural ODE support mini-batch, use it to boost your training progress.
