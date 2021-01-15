```
function makeIterator(arr) {
	let index = 0;
    return {
        next() {
            if(index < arr.length) {
            	return {
                    value: arr[index++],
                    done: false
            	}
            }
        }
    }
	return {
		value: undefined,
		done: true
	}
}
``` 