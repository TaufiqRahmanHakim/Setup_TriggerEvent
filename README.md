# TriggerEvent
TriggerEvent is component for easy event system setup and re-useable
# Source Code
##3d===============================
```csharp 
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Events;
​
public class TriggerSetup : MonoBehaviour
{
    [Tooltip("One time use")]
    [SerializeField] bool oneTimeUse;
    [Tooltip("Search only Tags")]
    [SerializeField] string tagFilter;
    [SerializeField] UnityEvent onTriggerEnter;
​
    [SerializeField] UnityEvent onTriggerStay;
​
    [SerializeField] UnityEvent onTriggerExit;
​
​
​
    private void OnTriggerEnter(Collider other)
    {
        if (!string.IsNullOrEmpty(tagFilter) && !other.gameObject.CompareTag(tagFilter)) return;
        onTriggerEnter.Invoke();
        if (oneTimeUse)
        {
            Destroy(this);
        }
    }
​
    private void OnTriggerStay(Collider other)
    {
        if (!string.IsNullOrEmpty(tagFilter) && !other.gameObject.CompareTag(tagFilter)) return;
        onTriggerStay.Invoke();
        if (oneTimeUse)
        {
            Destroy(this);
        }
    }
​
    private void OnTriggerExit(Collider other)
    {
        if (!string.IsNullOrEmpty(tagFilter) && !other.gameObject.CompareTag(tagFilter)) return;
        onTriggerExit.Invoke();
        if (oneTimeUse)
        {
            Destroy(this);
        }
    }
}
```
##2d===============================
```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Events;

public class TriggerSetup2d : MonoBehaviour
{
    [Tooltip("One time use")]
    [SerializeField] bool oneTimeUse;
    [Tooltip("Search only Tags")]
    [SerializeField] string tagFilter;
    [SerializeField] UnityEvent onTriggerEnter;

    [SerializeField] UnityEvent onTriggerStay;
    //
    [SerializeField] UnityEvent onTriggerExit;

    [SerializeField] UnityEvent onTriggerStayExit;

    private bool onTriggerStayExitFlag = false;

    private void Update()
    {
        if (onTriggerStayExitFlag)
        {
            onTriggerStayExit.Invoke();
        }
    }
    private void OnTriggerEnter2D(Collider2D other)
    {
        if (!string.IsNullOrEmpty(tagFilter) && !other.gameObject.CompareTag(tagFilter)) return;
        onTriggerEnter.Invoke();
        onTriggerStayExitFlag = false;
        if (oneTimeUse)
        {
            Destroy(this);
        }
    }

    private void OnTriggerStay2D(Collider2D other)
    {
        if (!string.IsNullOrEmpty(tagFilter) && !other.gameObject.CompareTag(tagFilter)) return;
        onTriggerStay.Invoke();
        if (oneTimeUse)
        {
            Destroy(this);
        }
    }

    private void OnTriggerExit2D(Collider2D other)
    {
        if (!string.IsNullOrEmpty(tagFilter) && !other.gameObject.CompareTag(tagFilter)) return;
        onTriggerExit.Invoke();
        onTriggerStayExitFlag = true;
        if (oneTimeUse)
        {
            Destroy(this);
        }
    }
}

```
# Preview

![tyhjtyjtuktuk](https://github.com/TaufiqRahmanHakim/Setup_TriggerEvent/assets/112629423/4542f8dd-0784-46ee-bc77-738e15eeef82)
