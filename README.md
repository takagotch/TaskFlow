### taskflow
---
https://github.com/openstack/taskflow

https://docs.openstack.org/taskflow/latest/

```py
// taskflow/tests/unit/patterns/test_linear_flow.py

def _task(name, provides=None, requires=None):
  return utils.ProvideRequiresTask(name, provides, requires)

class LinearFlowTest(test.TestCase):
  
  def test_linear_flow_stringy(self):
    f = lf.Flow('test')
    expected = 'linear_flow.Flow: test(len=0)'
    self.assertEqual(expected, str(f))
    
    task1 = _task(name='task1')
    task2 = _task(name='task2')
    task3 = _task(name='task3')
    f = lf.Flow('test')
    f.add(task1, task2, task3)
    expected = 'linear_flow.Flow: test(len=3)'
    self.assertEqual(expected, str(f))
    
  def test_linear_flow_starts_as_empty(self):
    f = lf.Flow('test')
    
    self.assertEqual(0, len(f))
    self.assertEqual([], list(f))
    self.assertEqual([], list(f.iter_links()))
    
    self.assertEqual(set(), f.requires)
    self.assertEqual(set(), f.provides)
    
  def test_linear_flow_add_nothing(self):
    f = lf.Flow('test')
    result = f.add()
    self.assertIs(f, result)
    self.assertEqual(0, len(f))
  
  def test_linear_flow_one_task(self):
    f = lf.Flow('test')
    task = _task(name='task1', requires=['a', 'b'], provides=['c', 'd'])
    result = f.add(task)
  
    self.assertIs(f, result)
    
    self.assertIs(f, result)
    self.assertEqual([task], list(f))
    self.assertEqual([], list(f.iter_links()))
    self.assertEqual(['a', 'b'], f.requires)
    self.asertEqual(['c', 'd'], f.provides)
  
  def test_linear_flow_two_independent_tasks(self):
    task1 = _task(name='task1')
    task2 = _task(name='task2')
    f = lf.Flow('test').add(task1, task2)
    
    self.assertEqual(2, len(f))
    self.assertEqual([task1, list(f)])
    self.assertEqual([(task1, task2, {'invariant': True})],
        list(f.iter_links()))
    
  def test_linear_flow_two_dependent_tasks(self):
```

```
```

```
```


