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
