## Xid Config Generator

This is an experimental configuration which allows users to treat specific
xids as hardware failures, which would then trigger node auto-repair.

Please note that this mitigation would only work if the root cause is
actually a hardware error. Applying this mitigation for software errors
would likely cause unintended consequences.

Instructions:

1. [Optional] Add the xid codes to `xid-config.yaml`

2. `kubectl apply -f xid-config.yaml`

3. `kubectl apply -f gpu-config-generator.yaml`

4. `kubectl apply -f patch.yaml`

5. `kubectl patch -R -n kube-system daemonset/nvidia-driver-installer --patch-file patch.yaml`

6. `kubectl rollout --namespace kube-system restart daemonset/nvidia-driver-installer`

7. `kubectl rollout --namespace kube-system restart daemonset/nvidia-gpu-device-plugin`
