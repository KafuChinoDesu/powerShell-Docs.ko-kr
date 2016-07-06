# Convert-String
**Convert-String**은 "자동 대체" 기능을 노출합니다. 텍스트가 어떻게 표시되는지에 대한 이전 및 이후 예제를 제공하면 **Convert-String**에서 자동으로 텍스트 서식을 지정합니다. 다음은 어떤 사람의 이름과 성을 가져오고 성, 쉼표, 성의 첫 이니셜 및 점으로 바꾸는 데모입니다. 정규식을 사용하여 시간이 얼마나 걸리는지 확인해 보세요.

```powershell
"Lee Holmes", "Steve Lee", "Jeffrey Snover" | Convert-String -Example "Bill Gates=Gates, B.","John Smith=Smith, J."

Holmes, L.
Lee, S.
Snover, J.
```


<!--HONumber=Jun16_HO4-->


