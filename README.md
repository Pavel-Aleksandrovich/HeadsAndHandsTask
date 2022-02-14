# HeadsAndHandsTask

/*
 Задача
 На входе функция получает параметр n - натуральное число. Необходимо сгенерировать n-массивов, заполнить их случайными числами, каждый массив имеет случайный размер. Размеры массивов не должны совпадать. Далее необходимо отсортировать массивы. Массивы с четным порядковым номером отсортировать по возрастанию, с нечетным порядковым номером - по убыванию. На выходе функция должна вернуть массив с отсортированными массивами.
 */

import Foundation

private func createUniqueSizeArray(arrays: Array<[Int]>, size: Int) -> Int {
    var uniqueSize = Int.random(in: 0...size)
    var i = 0
    
    while i < arrays.count - 1 {
        if uniqueSize == arrays[i].count {
            uniqueSize = Int.random(in: 0...size)
            i = 0
        } else {
            i += 1
        }
    }
    return uniqueSize
}

private func createUniqueArrayWithArrays(n: Int, size: Int, minValue: Int, maxValue: Int) -> [[Int]] {
    var arrays = Array<[Int]>(repeating: [], count: n)
    
    for j in 0..<n {
        
        let uniqueSize = createUniqueSizeArray(arrays: arrays, size: size)
        
        var uniqueArray = Array<Int>(repeating: 0, count: uniqueSize)
        
        for i in 0..<uniqueArray.count {
            uniqueArray[i] = Int.random(in: minValue...maxValue)
        }
        
        arrays[j] = uniqueArray
    }
    return arrays
}
// n - number of arrays
// size - max size of array
// minValue - min value of each element
// maxValue - max value of each element
func сreateArrays(n: Int, size: Int = 15, minValue: Int = 0, maxValue: Int = 100) -> [[Int]] {
    
    if n <= 0 {
        print("n must be > 0")
        return []
    }
    
    if size < n {
        print("size must be < n")
        return []
    }
    
    if minValue > maxValue {
        print("minValue must be <= maxValue")
        return []
    }
    
    var arrays = createUniqueArrayWithArrays(n: n, size: size, minValue: minValue, maxValue: maxValue)
    
    for i in 0...arrays.count-1 {
        if i % 2 == 0 {
            arrays[i].sort(){$0 < $1}
        } else {
            arrays[i].sort(){$0 > $1}
        }
    }
    
    return arrays
}

let arrays = сreateArrays(n: 11)
print(arrays)
