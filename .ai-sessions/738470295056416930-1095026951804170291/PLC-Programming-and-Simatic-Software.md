# PLC Programming and Simatic Software

## Simatic Step 7 Basic v19

### TIA Portal Licensing
- **License Status**: Available license for Simatic Step 7 Basic v19 has been identified within the organization
- **Basic License**: 
  - Compatible with S7-1200 series PLCs
  - Entry-level version of Simatic software suite
  - Suitable for standard automation projects
- **Professional License**: 
  - Required for S7-1500 series PLCs
  - Advanced features and expanded functionality
- **Version**: v19 (current generation)

### Compatibility Considerations
The compatibility and implementation steps for Simatic Step 7 Basic v19 depend on several factors:

#### Hardware Requirements
- Target PLC hardware compatibility with Step 7 Basic v19
- System requirements for development workstation
- Communication interface requirements

#### Project Requirements  
- Specific automation tasks and complexity
- Integration with existing systems
- Required programming languages (LAD, FBD, STL)

#### Implementation Steps (Detailed)
1. **Hardware Procurement**: Purchase Siemens PLC (S7-1212 G2 recommended for cost-effectiveness) - approximately €274
2. **Project Setup**: Create new TIA Portal project with the PLC and PN-PN Coupler
3. **Coupler Configuration**: 
   - If coupler is pre-configured, request connection instructions from machine builder
   - Machine builder should provide data mapping (what data is on what address)
4. **PLC Configuration**: Configure PLC to pull data from the coupler
5. **Programming**: Develop PLC logic using appropriate programming languages
6. **Testing**: Validate communication and data exchange
7. **Deployment**: Download and commission the system

## Hardware Recommendations

### Siemens S7-1200 Series
- **S7-1212 G2** (Recommended for cost-effectiveness):
  - **Cost**: ~€274 (~$300)
  - **Features**: Lowest cost Generation 2 S7-1200 PLC
  - **Memory**: Significantly more memory compared to G1 range
  - **Scalability**: Sufficient capacity for additional device connections
- **S7-1214 G2**:
  - **Cost**: ~€470 (~$515)  
  - **Use Case**: Higher I/O requirements
- **Compatible Software**: TIA Portal Basic License
- **Use Case**: Standard automation and data acquisition applications

### Communication Hardware
- **PN-PN Coupler**: For connecting multiple PLCs or networks
- **Configuration**: Should be handled by machine builder
- **Data Mapping**: Machine builder provides address mapping documentation

## Technical Documentation and Resources

### PN-PN Coupler Configuration
- **Siemens Official Guide**: [PN-PN Coupler Getting Started](https://support.industry.siemens.com/cs/document/88737127/pn-pn-coupler-getting-started?dti=0&lc=en-IE)
- **Technical Manual**: [PN_PN_Koppler_en.pdf](https://cache.industry.siemens.com/dl/files/436/23865436/att_926813/v1/PN_PN_Koppler_en.pdf)
- **Implementation Tutorial**: [Setup Communication Between Two PLCs via PN-PN Coupler](https://automationhowto.com/plc/how-to-setup-communication-between-two-plcs-via-siemens-pn-pn-coupler-in-tia-portal/)

### Key Implementation Notes
- **Multi-PLC Projects**: Can work without having both PLCs in the same TIA Portal project
- **Machine Builder Coordination**: Essential for coupler configuration and data mapping
- **Address Mapping**: Machine builder should provide documentation on data locations
- **Learning Opportunity**: If manufacturer denies support, this presents an excellent opportunity to learn Siemens PLC programming hands-on

## Critical Implementation Questions

### Data Access Requirements
- **DBX Addressing Documentation**: Will be provided by manufacturer specifically for the PN/PN coupler (not the machine's PLC)
- **Local PLC Access**: Available for direct communication
- **Server Extension Limitation**: Extension of PLC access to server infrastructure has been denied by manufacturer
- **Implementation Approach**: Adding dedicated S7-1200 PLC for PN/PN coupler data acquisition

## Project Feasibility and Site Infrastructure

### Management Approval Status
- **Single PLC Investment**: Management can be convinced to install 1 PLC for the project
- **Future Expansion Potential**: Site has 2 additional Siemens PLC machines that could utilize the solution in future
- **Cost Justification**: Multi-machine applicability helps justify initial investment

### Existing Hardware Assessment
- **Alternative Investigation**: Exploring existing hardware that might support Profinet with extension modules
- **Cost Optimization**: Leveraging existing infrastructure before purchasing new hardware
- **Extension Module Compatibility**: Some existing hardware may only need Profinet extension modules

### Profinet Master/Slave Architecture
- **Technical Question**: Does any Profinet Master work, but not a Slave?
- **Master Requirements**: Profinet Master devices can initiate communication and control network traffic
- **Slave Limitations**: Profinet Slave devices respond to Master requests but cannot initiate communication
- **Implementation Impact**: Master capability required for controlling PN-PN couplers and data acquisition

## Specific Use Case: Rack Rolling Machine

### Machine Details
- **Machine Type**: Rack rolling machine
- **Manufacturer Setup**: PN/PN coupler installed by manufacturer for data transfer
- **Data Integration**: Machine has integrated sensors and existing data systems

### Target Data Types
- **Process Data**:
  - Cycle time
  - Alarms
  - Part count
- **Tool Management**:
  - Tool ID
  - Tool life
- **Sensor Readings**: Various sensor data already integrated with the machine
- **User Interface**: Machine has existing screen for tool management display

### Data Acquisition Strategy
- **Primary Method**: S7-1200 PLC dedicated to PN/PN coupler communication
- **Data Source**: PN/PN coupler (not direct machine PLC access)
- **Documentation**: Manufacturer will provide coupler-specific DBX addressing

### Alternative Sensor Implementation
- **Independent Part Count Sensor**: Technical suggestion to add custom sensor for part counting
- **Derived Cycle Time**: Part count sensor data can be used to calculate cycle time
- **Current Transformer Monitoring**: Monitor spindle and axis motors to determine runtime
  - **Implementation**: Install current transformers on spindle and axis motor power lines
  - **Data Extraction**: Motor current patterns indicate machine operation status
  - **Runtime Calculation**: Active current periods determine actual machine runtime
  - **Reception**: Well-received as innovative approach, previously unconsidered solution
  - **Broader Applications**: Recognized as having potential for many different use cases beyond the immediate rack rolling machine project
- **Benefits**: 
  - Independent from manufacturer restrictions
  - Direct measurement without coupler dependency
  - Real-time data without contractual limitations
  - Non-invasive electrical monitoring
- **Implementation Considerations**:
  - Sensor placement and mounting
  - Integration with S7-1200 PLC
  - Calibration and validation against existing machine data
  - Current transformer sizing and installation safety

### SHARC Hardware Alternative
- **Product**: SHARC industrial automation device
- **Source**: Available from MRIIoT (https://mriiot.com/sharc)
- **Offer**: Hardware can be provided for evaluation/testing
- **Potential Use Case**: Alternative to Siemens PLC for data acquisition from industrial equipment
- **Consideration**: May provide different approach to manufacturer restriction challenges

### Alternative Network Access Considerations
- **Direct Network Connection**: Technical question about connecting network jack to access machine subnet directly
- **Access Denial Source Confirmed**: Denial is by the machine manufacturer
- **Company Decision**: Company decided against bypassing manufacturer restrictions
- **Contractual Implications**: Workarounds would violate AMC/Support contract terms
  - AMC: Annual Maintenance Contract
  - Support contract violations could affect warranty and service agreements
- **Implementation Impact**: Must work within manufacturer-approved methods only

### Regional Equipment Modification Policies
- **Equipment Origin Bias**: Company policies vary significantly based on equipment origin
  - **Local Machines**: Flexible modification policies
  - **Chinese/Taiwanese Machines**: Permissive approach to modifications
  - **European Machines**: Strict no-modification policies
- **Business Context**: Different risk tolerance and contractual relationships based on vendor region
- **Policy Implications**: EU equipment requires manufacturer-approved methods only
- **Support Service Risk**: Equipment modifications can result in support refusal ("we can't fix it because you touched it")
- **Business Impact**: Loss of technical support when equipment issues arise after modifications
- **Internal Expertise Gap**: 
  - EU predominantly uses Siemens equipment
  - Limited knowledge and support for Siemens devices within company umbrella
  - Applies to both PLCs and CNC machines
  - Increases reliance on external manufacturer support
- **Equipment Cost Considerations**:
  - EU machines are significantly more expensive than Asian/local alternatives
  - Higher equipment investment increases risk aversion for modifications
  - Cost factor compounds contractual and expertise concerns

## Management Decision Process

### Alternative Recommendations
- **Cost-Effective Solution Proposed**: Cheap PLC with minimal I/O capabilities for data acquisition
- **Data Coverage**: Most required data could be obtained through this simpler approach
- **Technical Feasibility**: Alternative sensor implementation would provide necessary metrics
- **Cost Benefits**: Significantly lower implementation cost compared to manufacturer involvement

### Management Decision
- **Final Choice**: Operations management decided to involve manufacturer despite alternative recommendations
- **Decision Context**: Chose manufacturer-approved route over cost-effective independent solution
- **Risk Assessment**: Management prioritized compliance and support over cost savings
- **Potential Workarounds**: Direct subnet access might bypass certain limitations depending on denial source
- **Implementation Considerations**:
  - Network security and access policies
  - Manufacturer warranty and support implications
  - Client internal policies and approval processes
  - Technical feasibility of direct subnet connection

## Network Architecture Considerations

### Single PLC to Multiple Couplers
- **Question**: Can 1 PLC connect to PN-PN couplers of multiple machines via network?
- **Answer**: Yes, this should work effectively
- **Key Technical Detail**: PN-PN couplers are treated as Profinet devices on the network
- **Network Topology**: Multiple PN-PN couplers can be connected through the same network infrastructure
- **Profinet Integration**: 
  - Couplers appear as standard Profinet devices to the PLC
  - Standard Profinet addressing and communication protocols apply
  - Network discovery and configuration through TIA Portal
- **Implementation Considerations**:
  - Profinet network configuration and device addressing
  - Standard Profinet communication protocols
  - Bandwidth and latency requirements for multiple devices
  - Network security considerations for industrial Profinet networks

## Alternative Solutions and Cost Considerations

### Operational Constraints
- **Team Expertise Gap**: Operations team lacks experience with Siemens PLCs
- **Cost Sensitivity**: $300 S7-1214 G2 may be too expensive for simple data acquisition
- **Use Case Scope**: Only needed for data extraction from coupler, not full automation control

### Alternative PLC Options
- **Technical Feasibility**: Any PLC speaking Profinet protocol should work for communicating with PN-PN couplers
- **Requirements**: Cheaper PLC alternatives that can communicate with PN-PN couplers
- **Protocol Support Needed**: 
  - OPC-UA
  - Modbus
  - MQTT
  - Any standard industrial communication protocol
- **Primary Function**: Data acquisition from coupler without full Siemens ecosystem complexity

### Siemens Ecosystem Advantages
- **Comprehensive Support**: Siemens provides excellent support for all their products
- **Use Case Documentation**: Well-documented implementations and troubleshooting resources
- **Product Integration**: Seamless integration between all Siemens devices and software
- **Technical Expertise**: Wider availability of training materials and specialized knowledge

### Evaluation Criteria  
- **Cost Comparison**: 
  - S7-1212 G2: €274 (most cost-effective Siemens option)
  - S7-1214 G2: €470 (higher I/O requirements)
  - Alternative PLCs: Should be lower cost for data acquisition only
- **Expertise Requirements**: Easier to implement without specialized Siemens PLC knowledge
- **Protocol Compatibility**: Must support communication with PN-PN couplers via Profinet
- **Functionality**: Data extraction and forwarding capabilities
- **Scalability**: Consider future expansion needs (S7-1212 G2 has sufficient memory for additional devices)

## CNC Integration and Connectivity

### Ladder99 Platform
- **Product Clarification**: Confirmed as NOT a MRIIoT product
- **Mitsubishi CNC Support**: Inquiry about driver availability for Mitsubishi CNC machines
- **Industrial Connectivity**: Related to broader industrial automation and machine connectivity solutions

### Mitsubishi CNC Connectivity Options
- **Windows SDK**: Mitsubishi provides a Windows-based software development kit
- **Documentation Availability**: Technical documentation can be shared upon request
- **Communication Protocols**:
  - **OPC-UA Addon**: Available but not extensively tested
  - **MTConnect Addon**: Available but implementation not followed up
- **Implementation Status**: Limited practical experience with these connectivity options
- **Resource Sharing**: Documentation can be provided for evaluation

### Site Deployment Context
- **Controller Model**: M80 controllers from Mitsubishi
- **Quantity**: Only 2 M80 controllers at current site
- **Business Priority**: Low management priority due to small deployment scale
- **Investment Justification**: Limited number of machines makes connectivity solutions less cost-effective

### Fanuc CNC Connectivity Solutions
- **Initial Solution**: Fanuc driver provided effective starting point for CNC data acquisition
- **Production Solution**: MTLink-i from Fanuc selected as final connectivity solution
- **Implementation Path**: Third-party driver for initial development, then official Fanuc hardware for production
- **Success Story**: Driver helped establish proof of concept before investing in official Fanuc hardware

#### MTLink-i Integration Experience
- **Support Requirements**: Requires significant support from Fanuc for proper integration
- **Implementation Challenges**: Integration process is challenging and complex
- **Developer-Friendly**: More approachable for software developers compared to traditional PLC/CNC interfaces
- **Learning Curve**: Substantial technical expertise and vendor support needed for successful deployment

### Related Topics
- [[CNC-Machine-Connectivity]] - Industrial automation connectivity
- Industrial automation software licensing
- PLC programming methodologies
- CNC machine data acquisition and connectivity solutions

---
*Knowledge captured from Discord conversation in channel 1095026951804170291*