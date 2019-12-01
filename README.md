![2019-12-01 122133](https://user-images.githubusercontent.com/26820006/69912077-ad356000-1435-11ea-914a-34cbbef29e33.png)
## Motivation 🔦


It would be great if you add this example to Tabs component. Recently, I ran into a problem how to transfer the underscore and paint Tab at the same time. I found not trivial solution and want to share it with comunity.

## Summary 💡
It would be great if you add somenthig like `startAdornmentProps/endAdornmentProps` for posotion of Tab highlighter.

## Examples 🌈
You can find working example [on this sandbox](https://codesandbox.io/s/colored-tabs-material-ui-237l7)
<details><summary><b>or just check a code below:</b></summary>

```
import React from "react";
import {
  makeStyles,
  withStyles,
  createStyles,
  Theme
} from "@material-ui/core/styles";
import Tabs from "@material-ui/core/Tabs";
import Tab from "@material-ui/core/Tab";
import Typography from "@material-ui/core/Typography";
import Box from "@material-ui/core/Box";

interface TabPanelProps {
  children?: React.ReactNode;
  index: any;
  value: any;
}

const VerticalColoredTab = withStyles({
  indicator: {
    width: "100%",
    background:
      "linear-gradient(to right,  #556cd6 0%,#556cd6 5%,#d5ecf0 5%,#d5ecf0 100%)",
    zIndex: 1
  }
})(Tabs);

const HorizontalColoredTab = withStyles({
  indicator: {
    height: "100%",
    background:
      "linear-gradient(to bottom, #556cd6 0%,#556cd6 10%,#d5ecf0 10%,#d5ecf0 100%)",
    zIndex: 1
  }
})(Tabs);

const ColoredTab = withStyles((theme: Theme) =>
  createStyles({
    root: {
      textTransform: "none",

      "&:hover": {
        opacity: 1
      },
      "&$selected": {
        fontWeight: theme.typography.fontWeightMedium,
        color: "#000",
        zIndex: 2
      }
    },
    selected: {}
  })
)((props: StyledTabProps) => <Tab disableRipple {...props} />);

interface StyledTabProps {
  label: string;
}

function TabPanel(props: TabPanelProps) {
  const { children, value, index, ...other } = props;

  return (
    <Typography
      component="div"
      role="tabpanel"
      hidden={value !== index}
      id={`vertical-tabpanel-${index}`}
      aria-labelledby={`vertical-tab-${index}`}
      {...other}
    >
      <Box p={3}>{children}</Box>
    </Typography>
  );
}

function a11yProps(index: any) {
  return {
    id: `vertical-tab-${index}`,
    "aria-controls": `vertical-tabpanel-${index}`
  };
}

const useStyles = makeStyles((theme: Theme) => ({
  layout: {
    display: "flex",
    flexDirection: "column",
    justifyContent: "space-around",
    alignItems: "center",
    width: "100vw",
    height: "100vh",
    overflow: "hidden"
  },
  rootVertical: {
    backgroundColor: theme.palette.background.paper,
    display: "flex",
    height: 224
  },
  rootHorizontal: {
    backgroundColor: theme.palette.background.paper,
    display: "flex",
    flexDirection: "column",
    width: 500
  },
  verticalTabDivider: {
    borderRight: `1px solid ${theme.palette.divider}`
  },
  horizontalTabDivider: {
    borderBottom: `1px solid ${theme.palette.divider}`
  }
}));

export default function VerticalTabs() {
  const classes = useStyles();
  const [value, setValue] = React.useState(0);

  const handleChange = (event: React.ChangeEvent<{}>, newValue: number) => {
    setValue(newValue);
  };

  return (
    <div className={classes.layout}>
      <div className={classes.rootVertical}>
        <VerticalColoredTab
          orientation="vertical"
          variant="scrollable"
          value={value}
          onChange={handleChange}
          aria-label="Vertical tabs example"
          className={classes.verticalTabDivider}
        >
          <ColoredTab label="Item One" {...a11yProps(0)} />
          <ColoredTab label="Item Two" {...a11yProps(1)} />
          <ColoredTab label="Item Three" {...a11yProps(2)} />
          <ColoredTab label="Item Four" {...a11yProps(3)} />
          <ColoredTab label="Item Five" {...a11yProps(4)} />
          <ColoredTab label="Item Six" {...a11yProps(5)} />
          <ColoredTab label="Item Seven" {...a11yProps(6)} />
        </VerticalColoredTab>
        <TabPanel value={value} index={0}>
          Item One
        </TabPanel>
        <TabPanel value={value} index={1}>
          Item Two
        </TabPanel>
        <TabPanel value={value} index={2}>
          Item Three
        </TabPanel>
        <TabPanel value={value} index={3}>
          Item Four
        </TabPanel>
        <TabPanel value={value} index={4}>
          Item Five
        </TabPanel>
        <TabPanel value={value} index={5}>
          Item Six
        </TabPanel>
        <TabPanel value={value} index={6}>
          Item Seven
        </TabPanel>
      </div>
      <div className={classes.rootHorizontal}>
        <HorizontalColoredTab
          orientation="horizontal"
          variant="scrollable"
          value={value}
          onChange={handleChange}
          aria-label="horizontal tabs example"
          className={classes.horizontalTabDivider}
        >
          <ColoredTab label="Item One" {...a11yProps(0)} />
          <ColoredTab label="Item Two" {...a11yProps(1)} />
          <ColoredTab label="Item Three" {...a11yProps(2)} />
          <ColoredTab label="Item Four" {...a11yProps(3)} />
          <ColoredTab label="Item Five" {...a11yProps(4)} />
          <ColoredTab label="Item Six" {...a11yProps(5)} />
          <ColoredTab label="Item Seven" {...a11yProps(6)} />
        </HorizontalColoredTab>
        <TabPanel value={value} index={0}>
          Item One
        </TabPanel>
        <TabPanel value={value} index={1}>
          Item Two
        </TabPanel>
        <TabPanel value={value} index={2}>
          Item Three
        </TabPanel>
        <TabPanel value={value} index={3}>
          Item Four
        </TabPanel>
        <TabPanel value={value} index={4}>
          Item Five
        </TabPanel>
        <TabPanel value={value} index={5}>
          Item Six
        </TabPanel>
        <TabPanel value={value} index={6}>
          Item Seven
        </TabPanel>
      </div>
    </div>
  );
}
```
</details>