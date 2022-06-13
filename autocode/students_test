package coverage

import (
	"os"
	"reflect"
	"testing"
	"time"
)

// DO NOT EDIT THIS FUNCTION
func init() {
	content, err := os.ReadFile("students_test.go")
	if err != nil {
		panic(err)
	}
	err = os.WriteFile("autocode/students_test", content, 0644)
	if err != nil {
		panic(err)
	}
}

// WRITE YOUR CODE BELOW
func PeopleMock() People {
	return People{
		Person{
			firstName: "Greg",
			lastName: "Popovich",
			birthDay: time.Time{},
		},
		{
			firstName: "Allen",
			lastName: "Iverson",
			birthDay: time.Time{},
		},
		{
			firstName: "Kevin",
			lastName: "Garnett",
			birthDay: time.Time{},
		},
	}
}


func TestPeopleLen(t *testing.T) {
	data := map[string]struct {
		Mock People
		Want int
	}{
		"success": {
			Mock: PeopleMock(),
			Want: 3,
		},
	}

	for testName, testCase := range data {
		i := testName 
		v := testCase
		t.Run(i, func(t *testing.T) {
			got := v.Mock.Len()
			if got != v.Want {
				t.Errorf("got %v, want %v", got, v.Want)
			}
		})
	}
	}

	func TestPeopleLess(t *testing.T) {
		tests := map[string]struct {
			Name string
			P    People
			I    int
			J    int
			Want bool
		}{
			"success": {
				Name: "Success people less",
				P: People{
					Person{
						firstName: "Ivan",
						lastName:  "Ivanov",
						birthDay:  time.Time{},
					},
					{
						firstName: "Oleg",
						lastName:  "Olegov",
						birthDay:  time.Time{},
					},
					{
						firstName: "Leha",
						lastName:  "Lehov",
						birthDay:  time.Time{},
					},
					{
						firstName: "Anna",
						lastName:  "Annova",
						birthDay:  time.Time{},
					},
					{
						firstName: "Zheny",
						lastName:  "Zhenev",
						birthDay:  time.Time{},
					}},
				I:    2,
				J:    1,
				Want: true,
			},
			"success 1": {
				Name: "Success equal birth day and firstname peoples",
				P: People{
					Person{
						firstName: "Ivan",
						lastName:  "Ivanov",
						birthDay:  time.Date(2000, time.April, 10, 0, 0, 0, 0, time.UTC),
					},
					{
						firstName: "Ivan",
						lastName:  "Olegov",
						birthDay:  time.Date(2000, time.April, 10, 0, 0, 0, 0, time.UTC),
					}},
				I:    0,
				J:    1,
				Want: true,
			},
			"success 2": {
				Name: "Success not equal birth day peoples",
				P: People{
					Person{
						firstName: "Ivan",
						lastName:  "Ivanov",
						birthDay:  time.Date(2010, time.December, 20, 0, 0, 0, 0, time.UTC),
					},
					{
						firstName: "Ivan",
						lastName:  "Olegov",
						birthDay:  time.Date(2000, time.April, 10, 0, 0, 0, 0, time.UTC),
					}},
				I:    0,
				J:    1,
				Want: true,
			},
			"error": {
				Name: "Error people less",
				P: People{
					Person{
						firstName: "Ivan",
						lastName:  "Ivanov",
						birthDay:  time.Time{},
					},
					{
						firstName: "Oleg",
						lastName:  "Olegov",
						birthDay:  time.Time{},
					},
					{
						firstName: "Leha",
						lastName:  "Lehov",
						birthDay:  time.Time{},
					},
					{
						firstName: "Anna",
						lastName:  "Annova",
						birthDay:  time.Time{},
					},
					{
						firstName: "Zheny",
						lastName:  "Zhenev",
						birthDay:  time.Time{},
					}},
				I:    2,
				J:    3,
				Want: false,
			},
		}
		for _, item := range tests {
			t.Run(item.Name, func(t *testing.T) {
				if got := item.P.Less(item.I, item.J); got != item.Want {
					t.Errorf("Less() = %v, want %v", got, item.Want)
				}
			})
		}
	}

func TestSwap(t *testing.T) {
	tData := map[string]struct{
		I int
		J int
		people People
		//Expected People
	}{
		"succes": {I: 0, J: 1,people: PeopleMock()},
	}
	for i, v := range tData {
		t.Run(i, func(t *testing.T) {
			iVal := v.people[v.I]
			jVal := v.people[v.J]
			v.people.Swap(v.I,v.J)
			if v.people[v.I] != jVal || v.people[v.J] != iVal {
				t.Errorf("want: %v got: %v", iVal, v.people[v.J])
			} 
		})
	}
}

////////////////////////////////////////////////////////////////////////////////////////////////////

func TestNewMatrix(t *testing.T) {
	data := map[string]struct {
		str string
		Expect *Matrix 
		ExpectedError bool
		}{
			"success": {
				str: "123\n456\n789",
				Expect: &Matrix{
					rows: 3,
					cols: 1,
					data: []int{123, 456, 789},
				},
			ExpectedError: false,
			},
			"error": {
				str: "got\nerr",
				Expect: nil,
				ExpectedError: true,
			},
			"error with wrong Matrix": {
				str: "1 2 3\n4 5 ",
				Expect: nil,
				ExpectedError: true,
			},
	}
	for i, v := range data {
		t.Run(i, func(t *testing.T) {
			got, err := New(v.str)
			if (err != nil) != v.ExpectedError {
				t.Errorf("got error %v, expect %v", got, v.ExpectedError)
			}
			if !reflect.DeepEqual(got, v.Expect) {
				t.Errorf("got %v, expect %v", got, v.Expect)
			}
		})
	}
}

func TestMatrixRows(t *testing.T) {
	type Fields struct {
		Rows, Cols int
		Data []int
	}
	data := map[string]struct{
		fields Fields
		Expect [][]int
	}{
		"seccess": {
			fields: Fields{
				Rows: 4,
				Cols: 4,
				Data: []int{1, 2, 3, 4, 11, 22, 33, 44, 10, 20, 30 ,40, 100, 200 ,300 ,400},
			},
			Expect: [][]int{{1, 2, 3, 4}, {11, 22, 33, 44}, {10, 20 ,30 ,40}, {100, 200, 300, 400}},
		},
	}
	for i, v := range data {
		t.Run(i, func(t *testing.T) {
			m := Matrix{
				rows: v.fields.Rows,
				cols: v.fields.Cols,
				data: v.fields.Data,
			}
			if got := m.Rows(); !reflect.DeepEqual(got, v.Expect) {
				t.Errorf("got: %v, want: %v", got, v.Expect)
			}
		})
	}
}

func TestMatrixCols(t *testing.T) {
	type Fields struct {
		Rows, Cols int
		Data []int
	}
	data := map[string]struct {

		fields Fields
		Expect [][]int  
	}{
		"success" : {
			fields: Fields{
				Rows: 2, 
				Cols: 3,
				Data: []int{1, 2, 3, 4, 5 , 6},
			},
			Expect: [][]int{{1, 4}, {2, 5}, {3, 6}},
		},
	}
	for i, v := range data {
		t.Run(i, func(t *testing.T) {
			m := Matrix{
				rows: v.fields.Rows,
				cols: v.fields.Cols,
				data: v.fields.Data,
			}
			if got := m.Cols(); !reflect.DeepEqual(got, v.Expect) {
				t.Errorf("got : %v, want: %v", got, v.Expect)
			}
		})
	}
}

func TestSet(t *testing.T) {
	type Fields struct {
		Rows, Cols int
		Data []int
	}

	type Field struct {
		Row int
		Col int
		Value int
	}
	data := map[string]struct {
		fields Fields
		field Field
		Expect bool
	}{
		"valid": {
			fields: Fields{
				Rows: 2,
				Cols: 2,
				Data: []int{1, 2, 3, 4},
			},
			field: Field{
				Row: 0,
				Col: 0,
				Value: 0,
			},
			Expect: true,
		},
		"invalid": {
			fields: Fields{
				Rows: 2,
				Cols: 2,
				Data: []int{1, 2, 3, 4},
			},
			field: Field{
				Row: 2,
				Col: 2,
				Value: 0,
			},
			Expect: false,
		},
	}
	for i, v := range data {
		t.Run(i, func(t *testing.T) {
			m := &Matrix{
				rows: v.fields.Rows,
				cols: v.fields.Cols,
				data: v.fields.Data,
			}
			if got := m.Set(v.field.Row, v.field.Col, v.field.Value); got != v.Expect {
				t.Errorf("got: %v, want: %v", got, v.Expect)
			}
		})
	}
}