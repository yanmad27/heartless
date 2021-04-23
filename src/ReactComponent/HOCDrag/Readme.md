#Usage

```
const [data, updateData] = useState([])
const array_move_item = (arr, old_index, new_index) => {
  if (new_index >= arr.length) {
    let k = new_index - arr.length + 1;
    while (k--) {
      arr.push(undefined);
    }
  }
  arr.splice(new_index, 0, arr.splice(old_index, 1)[0]);
  return arr;
};
```

```
  const moveCard = (id, afterId) => {
    const cardIndex = data.findIndex(x => x.id === id);
    const afterIndex = data.findIndex(x => x.id === afterId);

    let dataUpdate = array_move_item([...data], cardIndex, afterIndex)
    updateData(dataUpdate)
  };
```

```
<DndProvider backend={HTML5Backend}>
    {
      data.map((el) => {
      return (
          <CardDrag
            key={el.id}
            id={el.id}
            moveCard={moveCard}>
            <VideoScheduleItem
              handleUpdateItem={(field, value) => props.handleUpdateItem(el.id, field, value)}
              deleteItem={() => props.deleteItem(el.id)}
              data={el}/>
          </CardDrag>
          )
        }
      )
    }
</DndProvider>
```