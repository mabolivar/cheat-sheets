## `py-spy`

`py-spy` is a simple but powerful profiler and provides an interactive chart as ouput.

https://github.com/benfred/py-spy

## `pyinstrument`

`pyinstrument` is also a nice alternative

This script shows an example on how to test an API (it has a lot of clutter)

```python
from datetime import datetime  
  
import msgpack  
from api import production_fs_app  
from fastapi import APIRouter, BackgroundTasks, Response  
from fastapi.testclient import TestClient  
  
app = production_fs_app()  
  
router = APIRouter()  
  
TEST_REQUEST = {  
    "param1": ["",""],
    "param2": [3,100],
}  
  
  
PROFILE_ITERATIONS = 5000  
  
  
@router.get("/profile")  
async def profile_get(  
    background_tasks: BackgroundTasks,  
    iterations: int = PROFILE_ITERATIONS,  
):  
    return await profile(background_tasks, TEST_REQUEST, iterations)  
  
  
@router.post("/profile")  
async def profile(  
    background_tasks: BackgroundTasks,  
    test_request: dict,  # noqa: B008  
    iterations: int = PROFILE_ITERATIONS,  
):  
    from pyinstrument import Profiler  
  
    payload = msgpack.dumps(test_request)  
    invocations = [  
        route for route in app.router.routes if route.path == "/api/v2/invocations"  
    ][0].endpoint  
  
    profiler = Profiler(interval=0.001, async_mode=True)  
    profiler.start()  
    for _ in range(iterations):  
        await invocations(background_tasks, payload)  
    profiler.stop()  
  
    return Response(content=profiler.output_html(), media_type="text/html")  
  
  
app.include_router(router)  
  
if __name__ == "__main__":  
    with TestClient(app) as client:  
        res = client.get("/profile")  
  
    timestamp = datetime.now().strftime("%Y%m%d-%H%M%S")  
    filename = f"/tmp/profile-{timestamp}.html"  
  
    with open(filename, "w") as f:  
        f.write(res.text)  
    print(f"Saved profile to {filename}")  
  
    import subprocess  
  
    subprocess.call(["open", filename])
```

