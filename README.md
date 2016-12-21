# ReactNative-ListView-Demo
测试ReactNative的ListView<br>

1.粘性标题
----------
粘性标题是IOS特色，可以利用ReactNative为Android也创建相同的效果。<br>利用sectionId或者sectionData作为标题，renderSectionHeader方法来为每组数据渲染出一个粘性标题。<br>代码：<br>

    class Hello extends Component {
       constructor(props) {
           super(props);
            var ds = new ListView.DataSource({
                rowHasChanged: (r1, r2) =>  r1 !== r2,
                   sectionHeaderHasChanged:(s1,s2)=>s1!==s2});

            this.state = {
                dataSource: ds.cloneWithRowsAndSections(this.getData())
            };
        }
        getData=()=>{
            var count={'section1':['row1','row2','row3','row4'],
                     'section2':['row1','row2','row3','row4'],
                     'section3':['row1','row2','row3','row4'],
                     'section4':['row1','row2','row3','row4']}
            return count;
        }
        render() {
            return (
                <View style={{flex:1,paddingTop:50}}>
                <ListView dataSource={this.state.dataSource}
                          renderRow={(rowData) =>
                          <View>
                              <Text>{rowData}</Text>
                          </View>
                          }
                          renderSectionHeader={(sectionData,sectionId)=>
                              <Text>{sectionData}</Text>
                          }
                />
                </View>
            );
        }
    }


    AppRegistry.registerComponent('Hello', () => Hello);
    
    
    
其中renderSectionHeader中的两个参数sectionData和sectionId都可以作为粘性标题，sectionData为当前组的所有数据，sectionID则是当前组的标题。建议使用sectionId作为粘性标题。
2.粘性头部(ios)
---------

stickyHeaderIndices；<br>
此方法为ios专有，并且无法与renderSectionHeader共同使用。<br>代码：<br>


    render() {
        return (
            <View style={{flex:1,paddingTop:50}}>
            <ListView dataSource={this.state.dataSource}
                      renderRow={(rowData) =>
                      <View>
                          <Text>{rowData}</Text>
                      </View>
                      }
                      stickyHeaderIndices={[0,2]}
            />
            </View>
        );
    }
<br>
stickyHeaderIndices={[0]}代表第1位的item在滚动时可以固定在头部，若参数为多个，stickyHeaderIndices={[0,2]}则代表第1位先固定在头部，直到第三位item达到顶部时取代它。<br>

3.更复杂的排列
----------
由于ListView是直接继承于ScrollView的，所以拥有ScrollView的所有属性和方法。contentContainerStyle就可以为我们打造更加复杂的item排列方式.<br>代码：


        render() {
        return (
            <View style={{flex:1,paddingTop:50}}>
            <ListView dataSource={this.state.dataSource}
                      contentContainerStyle={{flexWrap:'wrap',flexDirection:'row',justifyContent:'space-around'}}
                      renderRow={(rowData, sectionID, rowID, highlightRow) =>
                      <View style={{height:40, margin:10}}>
                          <Text onPress={()=>{
                              highlightRow:(sectionID,rowID)
                          }}>{rowData}</Text>
                      </View>
                      }


            />
            </View>
        );
    }
<br>示例中在contentContainerStyle中可以利用flex布局打造类似于android中的GridView类似的结构，十分高效。
                      
                  
